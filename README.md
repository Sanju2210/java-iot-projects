# java-iot-projects
class Ride {
    int rideId;
    String pickup;
    String drop;
    double fare;

    Ride(int rideId, String pickup, String drop, double fare) {
        this.rideId = rideId;
        this.pickup = pickup;
        this.drop = drop;
        this.fare = fare;
    }

    void displayRide() {
        System.out.println("Ride ID: " + rideId +
                ", Pickup: " + pickup +
                ", Drop: " + drop +
                ", Fare: ₹" + fare);
    }
}

class Node {
    Ride ride;
    Node next;

    Node(Ride ride) {
        this.ride = ride;
        this.next = null;
    }
}

class RideBookingHistory {
    Node head;

    void addRide(Ride r) {
        Node newNode = new Node(r);

        if (head == null) {
            head = newNode;
            return;
        }

        Node temp = head;
        while (temp.next != null) {
            temp = temp.next;
        }

        temp.next = newNode;
    }

    void deleteLastRide() {
        if (head == null) {
            System.out.println("No rides available.");
            return;
        }

        if (head.next == null) {
            head = null;
            System.out.println("Last ride deleted.");
            return;
        }

        Node temp = head;
        while (temp.next.next != null) {
            temp = temp.next;
        }

        temp.next = null;
        System.out.println("Last ride deleted.");
    }

    void displayRides() {
        if (head == null) {
            System.out.println("No ride history found.");
            return;
        }

        Node temp = head;
        while (temp != null) {
            temp.ride.displayRide();
            temp = temp.next;
        }
    }

    void searchRide(String location) {
        Node temp = head;
        boolean found = false;

        while (temp != null) {
            if (temp.ride.pickup.equalsIgnoreCase(location) ||
                temp.ride.drop.equalsIgnoreCase(location)) {
                temp.ride.displayRide();
                found = true;
            }
            temp = temp.next;
        }

        if (!found) {
            System.out.println("No rides found for location: " + location);
        }
    }

    void reverseHistory() {
        reverseDisplay(head);
    }

    void reverseDisplay(Node node) {
        if (node == null) {
            return;
        }

        reverseDisplay(node.next);
        node.ride.displayRide();
    }
}

public class Main {
    public static void main(String[] args) {
        RideBookingHistory history = new RideBookingHistory();

        history.addRide(new Ride(101, "Bangalore", "Mysore", 1200));
        history.addRide(new Ride(102, "Chennai", "Pondicherry", 900));
        history.addRide(new Ride(103, "Hyderabad", "Warangal", 750));

        System.out.println("All Ride History:");
        history.displayRides();

        System.out.println("\nSearch Ride by Location (Chennai):");
        history.searchRide("Chennai");

        System.out.println("\nReverse Ride History:");
        history.reverseHistory();

        System.out.println("\nDeleting Last Ride:");
        history.deleteLastRide();

        System.out.println("\nUpdated Ride History:");
        history.displayRides();
    }
}
