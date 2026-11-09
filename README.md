
task 1:

#include <iostream>
#include <iomanip>
#include <string>
using namespace std;

const int SIZE = 10;

struct InventoryItem
{
    int itemCode;
    string itemName;
    double cost;
    double sellingPrice;
};

InventoryItem insertItem()
{
    InventoryItem item;

    cout << "Enter item name: ";
    cin >> ws;
    getline(cin, item.itemName);

    cout << "Enter item cost: ";
    cin >> item.cost;

    static int code = 3123;
    item.itemCode = code++;

    item.sellingPrice = item.cost * 1.40;

    return item;
}

void displayStock(const InventoryItem* items)
{
    cout << "\n";
    cout << left
         << setw(12) << "Item Code"
         << setw(20) << "Item Name"
         << setw(12) << "Cost"
         << setw(15) << "Selling Price"
         << endl;

    cout << string(59, '-') << endl;

    for (int i = 0; i < SIZE; i++)
    {
        cout << left
             << setw(12) << items[i].itemCode
             << setw(20) << items[i].itemName
             << setw(12) << fixed << setprecision(2)
             << items[i].cost
             << setw(15) << items[i].sellingPrice
             << endl;
    }
}

int main()
{
    InventoryItem inventory[SIZE];

    for (int i = 0; i < SIZE; i++)
    {
        cout << "\nEnter details for item "
             << i + 1 << endl;

        inventory[i] = insertItem();
    }

    displayStock(inventory);
    task 1 part 2:

    #include <iostream>
#include <iomanip>
#include <string>
#include <cctype>
using namespace std;

const int SIZE = 10;

struct InventoryItem
{
    string itemCode;
    string itemName;
    double cost;
    double sellingPrice;
};

InventoryItem insertItem()
{
    InventoryItem item;

    cout << "Enter item name: ";
    cin >> ws;
    getline(cin, item.itemName);

    cout << "Enter item cost: ";
    cin >> item.cost;

    static int code = 31203;

    string prefix = item.itemName.substr(0, 3);

    for (int i = 0; i < prefix.length(); i++)
    {
        prefix[i] = toupper(
            static_cast<unsigned char>(prefix[i])
        );
    }

    item.itemCode = prefix + "_" + to_string(code++);

    item.sellingPrice = item.cost * 1.40;

    return item;
}

void displayStock(const InventoryItem* items)
{
    cout << "\n";

    cout << left
         << setw(15) << "Item Code"
         << setw(20) << "Item Name"
         << setw(12) << "Cost"
         << setw(15) << "Selling Price"
         << endl;

    cout << string(62, '-') << endl;

    for (int i = 0; i < SIZE; i++)
    {
        cout << left
             << setw(15) << items[i].itemCode
             << setw(20) << items[i].itemName
             << setw(12) << fixed << setprecision(2)
             << items[i].cost
             << setw(15) << items[i].sellingPrice
             << endl;
    }
}

int main()
{
    InventoryItem inventory[SIZE];

    for (int i = 0; i < SIZE; i++)
    {
        cout << "\nEnter details for item "
             << i + 1 << endl;

        inventory[i] = insertItem();
    }

    displayStock(inventory);

    return 0;
}

task 2:

#include <iostream>
#include <iomanip>
using namespace std;

struct FeetInches
{
    int feet;
    int inches;
};

struct RoomDimension
{
    FeetInches length;
    FeetInches width;
};

double computeTheCarpetingCost(
    const RoomDimension& room,
    double pricePerSquareFoot)
{
    double length =
        room.length.feet + room.length.inches / 12.0;

    double width =
        room.width.feet + room.width.inches / 12.0;

    double area = length * width;

    return area * pricePerSquareFoot;
}

int main()
{
    int numberOfRooms;
    double pricePerSquareFoot;

    cout << "Enter number of rooms: ";
    cin >> numberOfRooms;

    if (numberOfRooms <= 0)
    {
        cout << "Invalid number of rooms!" << endl;
        return 0;
    }

    RoomDimension* rooms = new RoomDimension[numberOfRooms];

    cout << "Enter carpet price per square foot: ";
    cin >> pricePerSquareFoot;

    for (int i = 0; i < numberOfRooms; i++)
    {
        cout << "\nRoom " << i + 1 << endl;

        cout << "Enter length (feet inches): ";
        cin >> rooms[i].length.feet
            >> rooms[i].length.inches;

        cout << "Enter width (feet inches): ";
        cin >> rooms[i].width.feet
            >> rooms[i].width.inches;
    }

    int choice;

    do
    {
        cout << "\n===== CARPET MENU =====" << endl;
        cout << "1. Calculate cost of each room" << endl;
        cout << "2. Calculate total cost of all rooms" << endl;
        cout << "3. Exit" << endl;

        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice)
        {
            case 1:
            {
                for (int i = 0; i < numberOfRooms; i++)
                {
                    double cost = computeTheCarpetingCost(
                        rooms[i],
                        pricePerSquareFoot
                    );

                    cout << fixed << setprecision(2);

                    cout << "Room " << i + 1
                         << " Cost = Rs. "
                         << cost << endl;
                }

                break;
            }

            case 2:
            {
                double totalCost = 0;

                for (int i = 0; i < numberOfRooms; i++)
                {
                    totalCost += computeTheCarpetingCost(
                        rooms[i],
                        pricePerSquareFoot
                    );
                }

                cout << fixed << setprecision(2);

                cout << "Total Carpet Cost = Rs. "
                     << totalCost << endl;

                break;
            }

            case 3:
                cout << "Program terminated." << endl;
                break;

            default:
                cout << "Invalid choice! Try again." << endl;
        }

    } while (choice != 3);

    delete[] rooms;

    return 0;
}
    

    return 0;
}
