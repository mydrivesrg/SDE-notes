### Car Parking Application Design

#### 1. Requirements

- **Car Types:** SUV and Hatchback.
- **Counting:** Maintain a count of SUV and Hatchback cars entering the premises.
- **Payment Calculation:** Calculate payment based on rates:
  - Hatchback: ₹10/hour
  - SUV: ₹20/hour
- **Overflow Handling:** Hatchback cars can occupy SUV spaces if hatchback spaces are full, but at hatchback rates.
- **Exit Payment:** Inform the user of their payment at exit.
- **Admin Interface:** Admin can view all parked cars.

#### 2. System Components

1. **Car Class:** Represents a car with type, entry time, and exit time.
2. **ParkingLot Class:** Manages parking spaces, including counts and payment calculations.
3. **Admin Interface:** Allows viewing all parked cars.

#### 3. Class Design

##### Car Class

```java
public class Car {
    private String licensePlate;
    private CarType type;
    private long entryTime;
    private long exitTime;
    
    public Car(String licensePlate, CarType type, long entryTime) {
        this.licensePlate = licensePlate;
        this.type = type;
        this.entryTime = entryTime;
    }

    public String getLicensePlate() {
        return licensePlate;
    }

    public CarType getType() {
        return type;
    }

    public long getEntryTime() {
        return entryTime;
    }

    public void setExitTime(long exitTime) {
        this.exitTime = exitTime;
    }

    public long getExitTime() {
        return exitTime;
    }

    public long getParkingDuration() {
        return (exitTime - entryTime) / 3600000; // Duration in hours
    }
}
```

##### CarType Enum

```java
public enum CarType {
    SUV, HATCHBACK
}
```

##### ParkingLot Class

```java
import java.util.*;

public class ParkingLot {
    private int suvCapacity;
    private int hatchbackCapacity;
    private int suvCount;
    private int hatchbackCount;
    private Map<String, Car> parkedCars;

    private static final int HATCHBACK_RATE = 10;
    private static final int SUV_RATE = 20;

    public ParkingLot(int suvCapacity, int hatchbackCapacity) {
        this.suvCapacity = suvCapacity;
        this.hatchbackCapacity = hatchbackCapacity;
        this.suvCount = 0;
        this.hatchbackCount = 0;
        this.parkedCars = new HashMap<>();
    }

    public boolean parkCar(Car car) {
        if (car.getType() == CarType.HATCHBACK) {
            if (hatchbackCount < hatchbackCapacity) {
                hatchbackCount++;
            } else if (suvCount < suvCapacity) {
                suvCount++;
            } else {
                return false; // No space available
            }
        } else {
            if (suvCount < suvCapacity) {
                suvCount++;
            } else {
                return false; // No space available
            }
        }
        parkedCars.put(car.getLicensePlate(), car);
        return true;
    }

    public double exitCar(String licensePlate, long exitTime) {
        Car car = parkedCars.remove(licensePlate);
        if (car == null) {
            throw new IllegalArgumentException("Car not found");
        }

        car.setExitTime(exitTime);
        long duration = car.getParkingDuration();

        if (car.getType() == CarType.HATCHBACK) {
            hatchbackCount--;
            if (duration == 0) {
                return HATCHBACK_RATE;
            }
            return duration * HATCHBACK_RATE;
        } else {
            suvCount--;
            if (duration == 0) {
                return SUV_RATE;
            }
            return duration * SUV_RATE;
        }
    }

    public List<Car> getAllParkedCars() {
        return new ArrayList<>(parkedCars.values());
    }
}
```

##### Admin Interface

```java
public class Admin {
    private ParkingLot parkingLot;

    public Admin(ParkingLot parkingLot) {
        this.parkingLot = parkingLot;
    }

    public void viewAllParkedCars() {
        List<Car> cars = parkingLot.getAllParkedCars();
        for (Car car : cars) {
            System.out.println("License Plate: " + car.getLicensePlate() + ", Type: " + car.getType() + ", Entry Time: " + car.getEntryTime());
        }
    }
}
```

#### 4. Usage Example

```java
public class Main {
    public static void main(String[] args) {
        ParkingLot parkingLot = new ParkingLot(5, 10);
        Admin admin = new Admin(parkingLot);

        Car car1 = new Car("ABC123", CarType.SUV, System.currentTimeMillis());
        Car car2 = new Car("XYZ789", CarType.HATCHBACK, System.currentTimeMillis());

        parkingLot.parkCar(car1);
        parkingLot.parkCar(car2);

        // Simulate exit
        long exitTime = System.currentTimeMillis() + 3600000; // 1 hour later
        double payment1 = parkingLot.exitCar("ABC123", exitTime);
        double payment2 = parkingLot.exitCar("XYZ789", exitTime);

        System.out.println("Payment for car ABC123: " + payment1);
        System.out.println("Payment for car XYZ789: " + payment2);

        // Admin views all parked cars
        admin.viewAllParkedCars();
    }
}
```

This example provides a basic structure and functionality for a car parking system. It can be extended with more advanced features such as concurrency handling, persistent storage, and user interfaces for both admin and users.
