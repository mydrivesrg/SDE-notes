Here's a simplified system design for the next-generation parking lot system based on your requirements:

### System Components:
1. **Parking Lot Manager:**
   - Manages the overall functioning of the parking lot system.
   - Handles requests for creating a parking lot, adding floors, slots, parking vehicles, unparking vehicles, and displaying slot information.

2. **Parking Lot:**
   - Represents the actual physical parking lot with multiple floors and slots.
   - Maintains information about each floor, including the number of slots and the types of vehicles allowed on each slot.

3. **Floor:**
   - Represents a single floor within the parking lot.
   - Contains information about the slots available on that floor, such as slot number, type of vehicle allowed, and occupancy status.

4. **Slot:**
   - Represents an individual parking slot.
   - Contains information about the slot number, type of vehicle allowed, occupancy status, and the vehicle parked (if occupied).

5. **Vehicle:**
   - Represents a vehicle that can be parked in the parking lot.
   - Contains attributes like type (car, bike, truck), registration number, and color.

6. **Ticket:**
   - Represents a ticket issued when a vehicle is parked.
   - Contains information about the parking lot ID, floor number, slot number, and other relevant details.

### Workflow:
1. **Initialization:**
   - The system starts by creating a parking lot with a specific ID, number of floors, and slots per floor.

2. **Parking Vehicle:**
   - When a vehicle arrives, the system finds the first available slot based on the specified criteria (type, lowest floor, lowest slot number).
   - If a suitable slot is found, the vehicle is parked, a ticket is generated, and the slot occupancy status is updated.

3. **Unparking Vehicle:**
   - When a vehicle needs to leave, the system unparks the vehicle based on the provided ticket ID.
   - If the ticket is valid and the slot is occupied, the vehicle is unparked, and the slot occupancy status is updated.

4. **Displaying Slot Information:**
   - The system can display various slot information based on the user's request.
   - This includes the number of free slots, lists of free slots, and lists of occupied slots for each vehicle type on each floor.

### Class Diagram:
```
+-----------------+       +----------------+       +---------------+
| ParkingLot      |       | Floor          |       | Slot          |
+-----------------+       +----------------+       +---------------+
| id: String      |1     *| floorNumber: int|1     *| slotNumber: int|
| floors: Floor[] |<>------| slots: Slot[]  |<>------| vehicle: Vehicle|
+-----------------+       +----------------+       +---------------+
          |                         |
          |                         |
          |                         |
    +-----+------+           +------+------+
    | Vehicle    |           | Ticket      |
    +------------+           +-------------+
    | type: Enum |           | ticketId: String|
    | regNo: String|           | ...          |
    | color: String|           +-------------+
    +------------+
```

### Sequence of Actions:
1. User inputs commands such as create_parking_lot, park_vehicle, unpark_vehicle, and display.
2. The ParkingLotManager interprets these commands and delegates actions to the ParkingLot, Floor, Slot, Vehicle, and Ticket classes accordingly.
3. The system processes each action and provides output based on the command and input parameters.

This design separates concerns by defining clear responsibilities for each class and maintains modularity for accommodating new requirements or changes easily.

------------------
# Code:
```
import java.util.*;

// Enum for vehicle types
enum VehicleType {
    CAR,
    BIKE,
    TRUCK
}

// Class to represent a Vehicle
class Vehicle {
    private String regNo;
    private String color;
    private VehicleType type;

    public Vehicle(String regNo, String color, VehicleType type) {
        this.regNo = regNo;
        this.color = color;
        this.type = type;
    }

    // Getters and setters
    public String getRegNo() {
        return regNo;
    }

    public void setRegNo(String regNo) {
        this.regNo = regNo;
    }

    public String getColor() {
        return color;
    }

    public void setColor(String color) {
        this.color = color;
    }

    public VehicleType getType() {
        return type;
    }

    public void setType(VehicleType type) {
        this.type = type;
    }
}

// Class to represent a Slot
class Slot {
    private int slotNumber;
    private VehicleType type;
    private boolean occupied;
    private Vehicle parkedVehicle;

    public Slot(int slotNumber, VehicleType type) {
        this.slotNumber = slotNumber;
        this.type = type;
        this.occupied = false;
    }

    // Getters and setters
    public int getSlotNumber() {
        return slotNumber;
    }

    public void setSlotNumber(int slotNumber) {
        this.slotNumber = slotNumber;
    }

    public VehicleType getType() {
        return type;
    }

    public void setType(VehicleType type) {
        this.type = type;
    }

    public boolean isOccupied() {
        return occupied;
    }

    public void setOccupied(boolean occupied) {
        this.occupied = occupied;
    }

    public Vehicle getParkedVehicle() {
        return parkedVehicle;
    }

    public void setParkedVehicle(Vehicle parkedVehicle) {
        this.parkedVehicle = parkedVehicle;
    }
}

// Class to represent a Floor
class Floor {
    private int floorNumber;
    private List<Slot> slots;

    public Floor(int floorNumber) {
        this.floorNumber = floorNumber;
        this.slots = new ArrayList<>();
    }

    public void addSlot(Slot slot) {
        slots.add(slot);
    }

    public List<Slot> getFreeSlots(VehicleType type) {
        List<Slot> freeSlots = new ArrayList<>();
        for (Slot slot : slots) {
            if (!slot.isOccupied() && slot.getType() == type) {
                freeSlots.add(slot);
            }
        }
        return freeSlots;
    }

    public List<Slot> getOccupiedSlots(VehicleType type) {
        List<Slot> occupiedSlots = new ArrayList<>();
        for (Slot slot : slots) {
            if (slot.isOccupied() && slot.getType() == type) {
                occupiedSlots.add(slot);
            }
        }
        return occupiedSlots;
    }

    // Other methods for slot operations
}

// Class to represent a ParkingLot
class ParkingLot {
    private String parkingLotId;
    private int numFloors;
    private int numSlotsPerFloor;
    private List<Floor> floors;

    public ParkingLot(String parkingLotId, int numFloors, int numSlotsPerFloor) {
        this.parkingLotId = parkingLotId;
        this.numFloors = numFloors;
        this.numSlotsPerFloor = numSlotsPerFloor;
        this.floors = new ArrayList<>();
        initializeFloors();
    }

    private void initializeFloors() {
        for (int i = 1; i <= numFloors; i++) {
            Floor floor = new Floor(i);
            initializeSlots(floor);
            floors.add(floor);
        }
    }

    private void initializeSlots(Floor floor) {
        for (int i = 1; i <= numSlotsPerFloor; i++) {
            VehicleType type = determineSlotType(i);
            Slot slot = new Slot(i, type);
            floor.addSlot(slot);
        }
    }

    private VehicleType determineSlotType(int slotNumber) {
        if (slotNumber == 1) {
            return VehicleType.TRUCK;
        } else if (slotNumber <= 3) {
            return VehicleType.BIKE;
        } else {
            return VehicleType.CAR;
        }
    }

    public List<Slot> findFirstAvailableSlots(VehicleType type) {
        List<Slot> availableSlots = new ArrayList<>();
        for (Floor floor : floors) {
            List<Slot> freeSlots = floor.getFreeSlots(type);
            if (!freeSlots.isEmpty()) {
                availableSlots.addAll(freeSlots);
                break; // Break after finding the first available slot
            }
        }
        return availableSlots;
    }

    public void parkVehicle(Vehicle vehicle) {
        List<Slot> availableSlots = findFirstAvailableSlots(vehicle.getType());
        if (!availableSlots.isEmpty()) {
            Slot slot = availableSlots.get(0);
            slot.setOccupied(true);
            slot.setParkedVehicle(vehicle);
            System.out.println("Parked vehicle. Slot Number: " + slot.getSlotNumber());
        } else {
            System.out.println("Parking Lot Full. Cannot park vehicle.");
        }
    }

    // Other methods for parking, unparking, displaying slot info, etc.
}

// Main class to run the parking lot system
public class ParkingLotSystem {
    public static void main(String[] args) {
        // Example usage of the parking lot system
        ParkingLot parkingLot = new ParkingLot("PR1234", 2, 6);
        
        Vehicle car1 = new Vehicle("KA-01-DB-1234", "black", VehicleType.CAR);
        Vehicle car2 = new Vehicle("KA-02-CB-1334", "red", VehicleType.CAR);
        
        parkingLot.parkVehicle(car1);
        parkingLot.parkVehicle(car2);
    }
}
```
