# FoodieGo - Online Food Delivery Management System

A complete Spring Boot food delivery web app with 4 user roles (Customer, Restaurant Owner, Delivery Rider, Admin) using **.txt files** instead of a database.

## How to Run (IntelliJ IDEA)

1. Open the project folder in IntelliJ IDEA → "Open" → select the `food-delivery-system` folder.
2. Wait for Maven to download dependencies.
3. Run `FoodDeliverySystemApplication.java` (right-click → Run).
4. Open browser at: **http://localhost:8080**

### Default Admin login
- Email: `admin@foodiego.com`
- Password: `admin123`

### Sign up flows
- Customers: `/register?role=CUSTOMER`
- Restaurant Owners: `/register?role=OWNER`
- Riders: `/register?role=RIDER` ("Join as Rider" page)

## Tech Stack
Java 17, Spring Boot 3, Thymeleaf, Bootstrap 5, plain JS, .txt file storage.

## Project Structure
```
src/main/java/food_delivery_system
 ├─ controller/   (Auth, Restaurant, Food, Cart, Order, Payment, Review, Admin)
 ├─ model/        (User, Admin, Restaurant, Food, Cart, Order, Payment, Review)
 ├─ service/      (business logic for each domain)
 ├─ repository/   (text-file backed CRUD)
 └─ util/         (FileUtil)
src/main/resources
 ├─ templates/    (Thymeleaf HTML pages)
 ├─ static/css|js|images
 └─ data/         (.txt storage files)
```

## OOP Concepts
- **Encapsulation**: All models use private fields + getters/setters.
- **Inheritance**: `Admin` extends `User`.
- **Polymorphism**: Repositories share a common save/load file pattern; services override behavior.
- **Abstraction**: `FileUtil` hides file IO details from services.

## Google Maps setup

The owner restaurant location page and customer checkout page now use the Google Maps JavaScript API for pin-point location selection.

1. Create a Google Maps JavaScript API key in Google Cloud.
2. Enable these APIs for the key:
   - Maps JavaScript API
   - Directions API
3. Open `src/main/resources/application.properties` and replace:
   ```properties
   google.maps.api.key=YOUR_GOOGLE_MAPS_API_KEY
   ```
   with your real key.
4. Restart the Spring Boot app.

If the API key is not set, the app still allows manual latitude/longitude entry and Google Maps route links, but the interactive pin map will show a setup message.

## Google Maps location notes

The restaurant and checkout pages now use Google Maps. If `google.maps.api.key` is empty, the app still shows a no-key Google Maps preview and saves locations using manual latitude/longitude or the browser's current-location button.

For clickable map pin placement and draggable pins, set a real Google Maps JavaScript API key in `src/main/resources/application.properties` or run with the environment variable `GOOGLE_MAPS_API_KEY`.
