#include <stdio.h>

#include <string.h>

#define MAX_SEATS 10
// Structure to store passenger details
struct Passenger {
    char name[50];
    int age;
    int seatNumber;
};

// Global variables
struct Passenger passengers[MAX_SEATS];
int bookedSeats = 0;

// Function to book a ticket
void bookTicket() {
    if (bookedSeats >= MAX_SEATS) {
        printf("\n❌ All seats are booked! No more reservations available.\n");
        return;
    }

    printf("\n🚆 Railway Reservation System\n");
    printf("Enter passenger name: ");
    scanf(" %[^\n]", passengers[bookedSeats].name);
    printf("Enter passenger age: ");
    scanf("%d", &passengers[bookedSeats].age);

    passengers[bookedSeats].seatNumber = bookedSeats + 1; // Assign seat
    printf("✅ Ticket Booked! Seat Number: %d\n", passengers[bookedSeats].seatNumber);
    
    bookedSeats++;
}

// Function to display booked tickets
void displayTickets() {
    if (bookedSeats == 0) {
        printf("\n📌 No tickets booked yet!\n");
        return;
    }

    printf("\n🎫 Booked Tickets:\n");
    printf("--------------------------------------------------\n");
    printf("| Seat No. | Name                | Age          |\n");
    printf("--------------------------------------------------\n");

    for (int i = 0; i < bookedSeats; i++) {
        printf("| %-8d | %-20s | %-4d        |\n", passengers[i].seatNumber, passengers[i].name, passengers[i].age);
    }
    printf("--------------------------------------------------\n");
}

// Function to cancel a ticket
void cancelTicket() {
    if (bookedSeats == 0) {
        printf("\n❌ No tickets to cancel!\n");
        return;
    }

    int seatNo;
    printf("\n❌ Enter seat number to cancel: ");
    scanf("%d", &seatNo);

    int found = 0;
    for (int i = 0; i < bookedSeats; i++) {
        if (passengers[i].seatNumber == seatNo) {
            found = 1;
            printf("✅ Ticket for %s (Seat %d) cancelled successfully!\n", passengers[i].name, passengers[i].seatNumber);
            
            // Shift remaining bookings
            for (int j = i; j < bookedSeats - 1; j++) {
                passengers[j] = passengers[j + 1];
                passengers[j].seatNumber--; // Update seat numbers
            }
            bookedSeats--;
            break;
        }
    }

    if (!found) {
        printf("❌ Seat number %d not found!\n", seatNo);
    }
}

// Main function
int main() {
    int choice;

    while (1) {
        printf("\n🚉 Railway Reservation System");
        printf("\n1️⃣ Book Ticket");
        printf("\n2️⃣ View Booked Tickets");
        printf("\n3️⃣ Cancel Ticket");
        printf("\n4️⃣ Exit");
        printf("\nEnter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                bookTicket();
                break;
            case 2:
                displayTickets();
                break;
            case 3:
                cancelTicket();
                break;
            case 4:
                printf("\n🚆 Exiting... Thank you for using the Railway Reservation System!\n");
                return 0;
            default:
                printf("\n❌ Invalid choice! Please try again.\n");
        }
    }

    return 0;
}
