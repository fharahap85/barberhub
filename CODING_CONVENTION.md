# Coding Convention — BarberHub

## 1. General

- Use **English** for all code, comments, commit messages, and PRs
- No commented-out code — delete it
- No `dd()`, `var_dump()`, `console.log()` in committed code
- Max line length: **120 characters**

---

## 2. Backend (Laravel)

### Naming

| Item | Convention | Example |
|------|-----------|---------|
| Controller | `SingularController` | `BookingController` |
| Model | `Singular` | `Booking`, `Barber` |
| Migration | `snake_case` | `create_bookings_table` |
| Service | `SingularService` | `BookingService` |
| Repository | `SingularRepository` | `BookingRepository` |
| Request | `ActionRequest` | `StoreBookingRequest` |
| Resource | `SingularResource` | `BookingResource` |
| Route | `snake_case` | `/api/bookings` |
| Method | `camelCase` | `getAvailableSlots()` |
| Variable | `camelCase` | `$availableSlots` |
| Database column | `snake_case` | `booking_date` |

### Routing

- All routes under `/api` prefix
- Public routes in `routes/api.php` without auth middleware
- Protected routes grouped with `auth:sanctum` middleware
- Owner routes with `role:owner` middleware
- Admin routes with `role:super_admin` middleware
- No sensitive DB IDs exposed in URLs unless necessary
- Pagination required for all list endpoints (`?page=N`)
- API versioning via header or prefix for breaking changes

### Controller

```php
class BookingController extends Controller
{
    public function __construct(
        private readonly BookingService $bookingService
    ) {}

    public function store(StoreBookingRequest $request): JsonResponse
    {
        $booking = $this->bookingService->create(
            $request->user(),
            $request->validated()
        );

        return $this->success($booking, 'Booking created', 201);
    }
}
```

- Controllers are thin — delegate to Service layer
- Always type-hint dependencies in constructor
- Return via `$this->success()` / `$this->error()` macros

### API Response Format (per API Spec)

```
Success:    { success: true, message: "...", data: {} }
Created:    { success: true, message: "...", data: {} }  (HTTP 201)
Error:      { success: false, message: "..." }
Validation: { success: false, message: "...", errors: { field: [...] } } (HTTP 422)
Unauthorized: { success: false, message: "Unauthenticated" } (HTTP 401)
Forbidden:   { success: false, message: "Access denied" } (HTTP 403)
Not Found:   { success: false, message: "Data not found" } (HTTP 404)
```

### Service

- Business logic lives here
- One class per domain entity
- Methods return models, collections, or throw typed exceptions

### Repository

- Database queries live here
- One method per query intent
- Return Eloquent models, not arrays

### Validation

- Use FormRequest classes (one per action)
- Define `authorize()` for permission checks
- Define `rules()` for input validation

### Model

```php
class Booking extends Model
{
    use SoftDeletes;

    protected $fillable = [
        'tenant_id', 'customer_id', 'barber_id',
        'booking_date', 'booking_time', 'status', 'notes',
    ];

    protected $casts = [
        'booking_date' => 'date',
        'booking_time' => 'string',
    ];
}
```

- Always define `$fillable` or `$guarded`
- Always define `$casts`
- Always add `SoftDeletes` on business entities

### Migration

- Always up and `down` methods
- Add indexes on `tenant_id`, `booking_date`, `status`, etc.
- Use `foreignId()->constrained()->cascadeOnDelete()` for FK

---

## 3. Frontend (React + TypeScript)

### Naming

| Item | Convention | Example |
|------|-----------|---------|
| Component | `PascalCase` | `BookingCard` |
| Page | `PascalCase` | `BookingHistoryPage` |
| File | `PascalCase` | `BookingCard.tsx` |
| Hook | `camelCase` | `useBookings` |
| Store | `camelCase` | `useAuthStore` |
| Service | `camelCase` | `bookingService` |
| Type/Interface | `PascalCase` | `Booking` |
| Prop type | `ComponentNameProps` | `BookingCardProps` |
| Route path | `kebab-case` | `/booking-history` |

### Component

```tsx
interface BookingCardProps {
  booking: Booking;
  onCancel?: (id: string) => void;
}

export function BookingCard({ booking, onCancel }: BookingCardProps) {
  return (
    <Card>
      <CardTitle>{booking.barber.name}</CardTitle>
      <CardDescription>{formatDate(booking.bookingDate)}</CardDescription>
    </Card>
  );
}
```

- One component per file
- Props typed via interface, named `ComponentNameProps`
- Use functions, not classes
- Export named, not default

### Data Fetching

- Use TanStack Query for server state
- Use Zustand for client state (auth, UI)
- Axios instance with interceptors in `lib/axios.ts`

```ts
export function useBookings() {
  return useQuery({
    queryKey: ['bookings'],
    queryFn: () => bookingService.getAll(),
  });
}
```

### Store (Zustand)

```ts
interface AuthState {
  user: User | null;
  token: string | null;
  login: (email: string, password: string) => Promise<void>;
  logout: () => void;
}

export const useAuthStore = create<AuthState>((set) => ({
  user: null,
  token: null,
  login: async (email, password) => { /* ... */ },
  logout: () => set({ user: null, token: null }),
}));
```

### File Structure

```
src/
├── components/       # Reusable UI components
│   ├── ui/          # shadcn/ui primitives
│   └── shared/      # App-specific shared components
├── features/        # Feature modules (auth, booking, etc.)
│   └── booking/
│       ├── components/
│       ├── hooks/
│       └── pages/
├── layouts/
├── lib/             # Axios instance, utils, constants
├── stores/          # Zustand stores
├── types/           # Shared TypeScript types
└── router/
```

---

## 4. Git & Commits

### Branch naming
```
feat/nama-fitur-#<issue-number>
fix/nama-bug-#<issue-number>
chore/nama-tugas-#<issue-number>
refactor/nama-#<issue-number>
docs/nama-#<issue-number>
```

### Commit message
```
type: brief description (closes #<issue-number>)

- bullet point detail if needed
```

### PR title
```
type: brief description
```
PR body must include `Closes #<issue-number>`.

---

## 5. CSS (Tailwind)

- Use Tailwind utility classes, not custom CSS
- Custom styles only when Tailwind cannot achieve it
- Use shadcn/ui `cn()` helper for conditional classes
- Organize classes: layout → spacing → size → color → state

---

## 6. Testing

### Backend (Pest)
```php
it('prevents double booking', function () {
    $booking = Booking::factory()->create([
        'barber_id' => $barber->id,
        'booking_date' => '2026-08-15',
        'booking_time' => '10:00',
    ]);

    $response = $this->actingAs($customer)->postJson('/api/bookings', [
        'barber_id' => $barber->id,
        'booking_date' => '2026-08-15',
        'booking_time' => '10:00',
    ]);

    $response->assertStatus(422);
    $response->assertJson(['success' => false]);
});
```

### Frontend (Vitest)
```ts
it('renders booking card', () => {
  render(<BookingCard booking={mockBooking} />);
  expect(screen.getByText('John')).toBeInTheDocument();
});
```
