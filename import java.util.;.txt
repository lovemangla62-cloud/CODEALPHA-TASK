import java.util.*;

class Room {
    int roomNo;
    String category;
    int price;
    boolean available;

    Room(int roomNo, String category, int price) {
        this.roomNo = roomNo;
        this.category = category;
        this.price = price;
        this.available = true;
    }
}

class Booking {
    int bookingId;
    String customerName;
    Room room;

    Booking(int bookingId, String customerName, Room room) {
        this.bookingId = bookingId;
        this.customerName = customerName;
        this.room = room;
    }
}

public class codealpha_HotelBookingSystem {

    static ArrayList<Room> rooms = new ArrayList<>();
    static ArrayList<Booking> bookings = new ArrayList<>();
    static int bookingCounter = 1001;

    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        // Adding Rooms
        rooms.add(new Room(101, "Standard", 2000));
        rooms.add(new Room(102, "Standard", 2000));
        rooms.add(new Room(201, "Deluxe", 4000));
        rooms.add(new Room(202, "Deluxe", 4000));
        rooms.add(new Room(301, "Suite", 7000));
        rooms.add(new Room(302, "Suite", 7000));

        while (true) {

            System.out.println("===== HOTEL BOOKING SYSTEM =====");
            System.out.println("1. Search Rooms");
            System.out.println("2. Book Room");
            System.out.println("3. View Bookings");
            System.out.println("4. Cancel Booking");
            System.out.println("5. Exit");
            System.out.print("Enter Choice: ");

            int choice = sc.nextInt();
            sc.nextLine();

            switch (choice) {

                case 1:
                    System.out.print("Enter Category (Standard/Deluxe/Suite): ");
                    String category = sc.nextLine();

                    System.out.println("Available Rooms:");
                    boolean found = false;

                    for (Room room : rooms) {
                        if (room.category.equalsIgnoreCase(category)
                                && room.available) {

                            System.out.println("Room No: " + room.roomNo +
                                    " | Price: " + room.price);
                            found = true;
                        }
                    }

                    if (!found) {
                        System.out.println("No rooms available.");
                    }
                    break;

                case 2:
                    System.out.print("Enter Customer Name: ");
                    String name = sc.nextLine();

                    System.out.print("Enter Room Number: ");
                    int roomNo = sc.nextInt();
                    sc.nextLine();

                    Room selectedRoom = null;

                    for (Room room : rooms) {
                        if (room.roomNo == roomNo && room.available) {
                            selectedRoom = room;
                            break;
                        }
                    }

                    if (selectedRoom == null) {
                        System.out.println("Room not available!");
                        break;
                    }

                    System.out.println("Room Category: " + selectedRoom.category);
                    System.out.println("Room Price: " + selectedRoom.price);

                    System.out.print("Confirm Booking (yes/no): ");
                    String confirm = sc.nextLine();

                    if (!confirm.equalsIgnoreCase("yes")) {
                        System.out.println("Booking Cancelled.");
                        break;
                    }

                    // Payment Simulation
                    System.out.println("Processing Payment...");
                    System.out.println("Payment Successful!");

                    selectedRoom.available = false;

                    Booking booking = new Booking(
                            bookingCounter++,
                            name,
                            selectedRoom);

                    bookings.add(booking);

                    System.out.println("Booking Successful!");
                    System.out.println("Booking ID: " + booking.bookingId);
                    break;

                case 3:
                    if (bookings.isEmpty()) {
                        System.out.println("No bookings found.");
                    } else {

                        for (Booking b : bookings) {

                            System.out.println("\nBooking ID: " + b.bookingId);
                            System.out.println("Customer: " + b.customerName);
                            System.out.println("Room No: " + b.room.roomNo);
                            System.out.println("Category: " + b.room.category);
                            System.out.println("Price: " + b.room.price);
                        }
                    }
                    break;

                case 4:
                    System.out.print("Enter Booking ID: ");
                    int bookingId = sc.nextInt();

                    boolean cancelled = false;

                    for (int i = 0; i < bookings.size(); i++) {

                        if (bookings.get(i).bookingId == bookingId) {

                            bookings.get(i).room.available = true;
                            bookings.remove(i);

                            System.out.println("Booking Cancelled Successfully!");
                            cancelled = true;
                            break;
                        }
                    }

                    if (!cancelled) {
                        System.out.println("Booking Not Found!");
                    }
                    break;

                case 5:
                    System.out.println("Thank You!");
                    sc.close();
                    System.exit(0);

                default:
                    System.out.println("Invalid Choice!");
            }
        }
    }
}