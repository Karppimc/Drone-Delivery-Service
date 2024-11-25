# Drone Delivery System - Service-Based Architecture
- Further project done from this can be seen here: https://github.com/Karppimc/Distributed-Drone-Delivery
- This project consists of two independent services that manage drones and handle delivery requests. The services are:
1. **DroneInventoryService** - Manages the fleet of drones.
2. **DeliveryService** - Manages delivery requests and assigns drones from the inventory.

## Prerequisites

- **Java 17** or later
- **Maven** for building and running the project
- **Git** for version control (if cloning the project)

## Running the Services

To run both services, you will need to open multiple terminal windows.

### Step 1: Start the DroneInventoryService

1. Open a new terminal window.
2. Navigate to the `DroneInventoryService` directory:
   ```bash
   cd path/to/drone-delivery-service-based/DroneInventoryService
   ```
3. Start the service:
   ```bash
   mvn spring-boot:run
   ```
   - The service will start on **port 8081**.

### Step 2: Start the DeliveryService

1. Open another terminal window.
2. Navigate to the `DeliveryService` directory:
   ```bash
   cd path/to/drone-delivery-service-based/DeliveryService
   ```
3. Start the service:
   ```bash
   mvn spring-boot:run
   ```
   - The service will start on **port 8082**.

## Testing the Services

Once both services are running, open a third terminal window to execute `curl` commands to interact with the services.

### Testing DroneInventoryService (Port 8081)

1. **Add a Drone**
   ```bash
   curl -d '{"id":"123", "name":"Tom-v1", "capacity":300}' -H "Content-Type: application/json" -X POST http://localhost:8081/dronora/drones
   ```

2. **Get All Drones**
   ```bash
   curl http://localhost:8081/dronora/drones
   ```

3. **Get a Specific Drone by ID**
   ```bash
   curl http://localhost:8081/dronora/drones/123
   ```

4. **Delete a Drone**
   ```bash
   curl -X DELETE http://localhost:8081/dronora/drones/123
   ```

### Testing DeliveryService (Port 8082)

> **Note:** Before creating a delivery, ensure that a drone is available in **DroneInventoryService**. Use the "Add a Drone" command above if needed.

1. **Create a Delivery** (assigning an available drone to the delivery):
   ```bash
   curl -d '{"id":"D001", "pickupLocation":"Location A", "dropoffLocation":"Location B", "droneId":"123"}' -H "Content-Type: application/json" -X POST http://localhost:8082/dronora/deliveries
   ```

2. **Get All Deliveries**
   ```bash
   curl http://localhost:8082/dronora/deliveries
   ```

3. **Get a Specific Delivery by ID**
   ```bash
   curl http://localhost:8082/dronora/deliveries/D001
   ```

4. **Delete a Delivery**
   ```bash
   curl -X DELETE http://localhost:8082/dronora/deliveries/D001
   ```

## Project Structure

```
drone-delivery-service-based/
├── DroneInventoryService/       # Manages drone inventory (CRUD operations)
│   ├── src/                     # Source code for DroneInventoryService
│   └── pom.xml                  # Maven configuration for DroneInventoryService
└── DeliveryService/             # Manages delivery requests
    ├── src/                     # Source code for DeliveryService
    └── pom.xml                  # Maven configuration for DeliveryService
```

## Summary

This setup demonstrates a **service-based architecture** where:
- **DroneInventoryService** independently manages drone data.
- **DeliveryService** interacts with **DroneInventoryService** to assign drones to delivery requests.

Both services function independently but work together to support a drone delivery system.
