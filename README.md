# task-3
hotel resevation system
mport java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

class Room {
    int roomNumber;
    String roomType;
    double price;
    boolean availability;

    public Room(int roomNumber, String roomType, double price) {
        this.roomNumber = roomNumber;
        this.roomType = roomType;
        this.price = price;
        this.availability = true;
    }
}

class Reservation {
    int reservationId;
    Room room;
    String guestName;
    String arrivalDate;
    String departureDate;

    public Reservation(int reservationId, Room room, String guestName, String arrivalDate, String departureDate) {
        this.reservationId = reservationId;
        this.room = room;
        this.guestName = guestName;
        this.arrivalDate = arrivalDate;
        this.departureDate = departureDate;
    }
}

public class HotelReservationSystem {
    List<Room> rooms = new ArrayList<>();
    List<Reservation> reservations = new ArrayList<>();
    int reservationIdCounter = 1;

    public static void main(String[] args) {
        HotelReservationSystem hotel = new HotelReservationSystem();
        hotel.run();
    }

    public void run() {
        Scanner scanner = new Scanner(System.in);

        // Initialize rooms
        rooms.add(new Room(1, "Single", 100.0));
        rooms.add(new Room(2, "Double", 200.0));
        rooms.add(new Room(3, "Suite", 500.0));

        while (true) {
            System.out.println("1. Search Rooms");
            System.out.println("2. Make Reservation");
            System.out.println("3. View Booking Details");
            System.out.println("4. Exit");
            System.out.print("Choose an option: ");
            int option = scanner.nextInt();
            scanner.nextLine(); // Consume newline left-over

            switch (option) {
                case 1:
                    searchRooms();
                    break;
                case 2:
                    makeReservation(scanner);
                    break;
                case 3:
                    viewBookingDetails();
                    break;
                case 4:
                    System.exit(0);
                    break;
                default:
                    System.out.println("Invalid option. Please choose again.");
            }
        }
    }

    public void searchRooms() {
        System.out.println("Available Rooms:");
        for (Room room : rooms) {
            if (room.availability) {
                System.out.println("Room Number: " + room.roomNumber + ", Room Type: " + room.roomType + ", Price: " + room.price);
            }
        }
    }

    public void makeReservation(Scanner scanner) {
        System.out.print("Enter room number: ");
        int roomNumber = scanner.nextInt();
        scanner.nextLine(); // Consume newline left-over
        Room room = getRoom(roomNumber);

        if (room != null && room.availability) {
            System.out.print("Enter guest name: ");
            String guestName = scanner.nextLine();
            System.out.print("Enter arrival date: ");
            String arrivalDate = scanner.nextLine();
            System.out.print("Enter departure date: ");
            String departureDate = scanner.nextLine();

            Reservation reservation = new Reservation(reservationIdCounter++, room, guestName, arrivalDate, departureDate);
            reservations.add(reservation);
            room.availability = false;

            System.out.println("Reservation successful. Reservation ID: " + reservation.reservationId);
        } else {
            System.out.println("Room not available.");
        }
    }

    public void viewBookingDetails() {
        System.out.println("Booking Details:");
        for (Reservation reservation : reservations) {
            System.out.println("Reservation ID: " + reservation.reservationId);
            System.out.println("Room Number: " + reservation.room.roomNumber);
            System.out.println("Guest Name: " + reservation.guestName);
            System.out.println("Arrival Date: " + reservation.arrivalDate);
            System.out.println("Departure Date: " + reservation.departureDate);
            System.out.println();
        }
    }

    public Room getRoom(int roomNumber) {
        for (Room room : rooms) {
            if (room.roomNumber == roomNumber) {
                return room;
            }
        }
        return null;
    }
}
