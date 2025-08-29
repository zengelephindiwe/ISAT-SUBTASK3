#include <iostream>
#include <string>
using namespace std;

const int MAX_ORDERS = 50;

// Parallel arrays
string orderIDs[MAX_ORDERS];
string customerNames[MAX_ORDERS];
int numMagwinya[MAX_ORDERS];
float totalCost[MAX_ORDERS];

// Current number of orders
int orderCount = 10; // already initialized with 10 orders

// Initialize sample data
void initializeData() {
    string initIDs[10]   = {"101","102","103","104","105","106","107","108","109","110"};
    string initNames[10] = {"Thabo","Lerato","Nomvula","Sipho","Bongani","Lindiwe","Jabulani","Ayanda","Kgosi","Refilwe"};
    int initNum[10]      = {3,5,2,4,6,1,3,2,6,4};
    float initCost[10]   = {15.75,30.50,10.00,22.00,40.25,5.50,18.00,12.75,28.00,24.50};

    for (int i = 0; i < 10; i++) {
        orderIDs[i] = initIDs[i];
        customerNames[i] = initNames[i];
        numMagwinya[i] = initNum[i];
        totalCost[i] = initCost[i];
    }

    // initialize remaining empty slots
    for (int i = 10; i < MAX_ORDERS; i++) {
        orderIDs[i] = "0";
        customerNames[i] = "";
        numMagwinya[i] = 0;
        totalCost[i] = 0.0;
    }
}

// Add new order
void addOrder() {
    if (orderCount >= MAX_ORDERS) {
        cout << "Error: Maximum number of orders (50) reached.\n";
        return;
    }

    string name;
    int quantity;
    float pricePerMagwinya = 5.25; // Example fixed price

    cout << "Enter customer name: ";
    cin >> name;
    cout << "Enter number of Magwinyas ordered: ";
    cin >> quantity;

    // Generate next order ID
    int lastID = stoi(orderIDs[orderCount - 1]);
    int newID = lastID + 1;

    orderIDs[orderCount] = to_string(newID);
    customerNames[orderCount] = name;
    numMagwinya[orderCount] = quantity;
    totalCost[orderCount] = quantity * pricePerMagwinya;

    cout << "Order added successfully! Order ID: " << newID << endl;
    orderCount++;
}

// Display all orders
void displayOrders() {
    cout << "\n--- All Orders ---\n";
    for (int i = 0; i < orderCount; i++) {
        if (orderIDs[i] != "0") {
            cout << "Order ID: " << orderIDs[i]
                 << ", Customer: " << customerNames[i]
                 << ", Magwinyas: " << numMagwinya[i]
                 << ", Total Cost: R" << totalCost[i] << endl;
        }
    }
}

// Find order by ID
void findOrder() {
    string searchID;
    cout << "Enter Order ID to search: ";
    cin >> searchID;

    bool found = false;
    for (int i = 0; i < orderCount; i++) {
        if (orderIDs[i] == searchID) {
            cout << "Order Found!\n";
            cout << "Order ID: " << orderIDs[i]
                 << ", Customer: " << customerNames[i]
                 << ", Magwinyas: " << numMagwinya[i]
                 << ", Total Cost: R" << totalCost[i] << endl;
            found = true;
            break;
        }
    }

    if (!found) {
        cout << "Order with ID " << searchID << " not found.\n";
    }
}

// Calculate total revenue
void calculateRevenue() {
    float sum = 0.0;
    for (int i = 0; i < orderCount; i++) {
        sum += totalCost[i];
    }
    cout << "Total Revenue: R" << sum << endl;
}

// Main menu
int main() {
    initializeData();

    int choice;
    do {
        cout << "\n--- Magwinya Order Management ---\n";
        cout << "1. Add New Order\n";
        cout << "2. Display All Orders\n";
        cout << "3. Find Order by ID\n";
        cout << "4. Calculate Total Revenue\n";
        cout << "5. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch(choice) {
            case 1: addOrder(); break;
            case 2: displayOrders(); break;
            case 3: findOrder(); break;
            case 4: calculateRevenue(); break;
            case 5: cout << "Exiting program...\n"; break;
            default: cout << "Invalid choice. Try again.\n";
        }
    } while(choice != 5);

    return 0;
}
