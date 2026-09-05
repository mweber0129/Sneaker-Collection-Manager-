# Sneaker-Collection-Manager-
numerations and structures
// ============================================================
// Sneaker Collection Manager - Part 1
// A C++ console application that manages a small sneaker
// collection using enumerations and structures.
// ============================================================

#include <iostream>
#include <string>
#include <iomanip>
#include <limits>
using namespace std;

// ------------------------------------------------------------
// Part 1 - Brand Enumeration
// ------------------------------------------------------------
enum SneakerBrand
{
    Nike,
    Adidas,
    Jordan,
    NewBalance,
    Puma
};

// ------------------------------------------------------------
// Part 2 - Condition Enumeration
// ------------------------------------------------------------
enum SneakerCondition
{
    New,
    Excellent,
    Good,
    Fair,
    Poor
};

// ------------------------------------------------------------
// Part 3 - Sneaker Structure
// ------------------------------------------------------------
struct Sneaker
{
    string model;
    SneakerBrand brand;
    double size;
    SneakerCondition condition;
    double purchasePrice;
    double estimatedValue;
};

// ------------------------------------------------------------
// Helper Functions
// ------------------------------------------------------------

// Converts a SneakerBrand enum value into a readable string.
string brandToString(SneakerBrand brand)
{
    switch (brand)
    {
        case Nike:       return "Nike";
        case Adidas:     return "Adidas";
        case Jordan:     return "Jordan";
        case NewBalance: return "New Balance";
        case Puma:       return "Puma";
        default:         return "Unknown";
    }
}

// Converts a SneakerCondition enum value into a readable string.
string conditionToString(SneakerCondition condition)
{
    switch (condition)
    {
        case New:       return "New";
        case Excellent: return "Excellent";
        case Good:      return "Good";
        case Fair:      return "Fair";
        case Poor:      return "Poor";
        default:        return "Unknown";
    }
}

// Prompts the user to select a brand from a numbered list and
// returns the corresponding SneakerBrand value.
SneakerBrand getBrandInput()
{
    int choice = 0;

    cout << "Select a brand:" << endl;
    cout << "1. Nike" << endl;
    cout << "2. Adidas" << endl;
    cout << "3. Jordan" << endl;
    cout << "4. New Balance" << endl;
    cout << "5. Puma" << endl;
    cout << "Enter choice (1-5): ";
    cin >> choice;

    // Keep asking until the user enters a valid option.
    while (choice < 1 || choice > 5)
    {
        cout << "Invalid choice. Please enter a number 1-5: ";
        cin >> choice;
    }

    switch (choice)
    {
        case 1: return Nike;
        case 2: return Adidas;
        case 3: return Jordan;
        case 4: return NewBalance;
        default: return Puma;
    }
}

// Prompts the user to select a condition from a numbered list and
// returns the corresponding SneakerCondition value.
SneakerCondition getConditionInput()
{
    int choice = 0;

    cout << "Select a condition:" << endl;
    cout << "1. New" << endl;
    cout << "2. Excellent" << endl;
    cout << "3. Good" << endl;
    cout << "4. Fair" << endl;
    cout << "5. Poor" << endl;
    cout << "Enter choice (1-5): ";
    cin >> choice;

    while (choice < 1 || choice > 5)
    {
        cout << "Invalid choice. Please enter a number 1-5: ";
        cin >> choice;
    }

    switch (choice)
    {
        case 1: return New;
        case 2: return Excellent;
        case 3: return Good;
        case 4: return Fair;
        default: return Poor;
    }
}

// Part 5 - Collects all information for a single sneaker from the user.
Sneaker getSneakerInput(int sneakerNumber)
{
    Sneaker s;

    cout << "\n--------------------------------" << endl;
    cout << "Enter information for Sneaker #" << sneakerNumber << endl;
    cout << "--------------------------------" << endl;

    cout << "Model Name: ";
    getline(cin, s.model);

    s.brand = getBrandInput();

    cout << "Size: ";
    cin >> s.size;

    s.condition = getConditionInput();

    cout << "Purchase Price: $";
    cin >> s.purchasePrice;

    cout << "Estimated Current Value: $";
    cin >> s.estimatedValue;

    // Clear the leftover newline so the next getline() call
    // (for the next sneaker's model name) works correctly.
    cin.ignore(numeric_limits<streamsize>::max(), '\n');

    return s;
}

// Displays the information for a single sneaker.
void displaySneaker(const Sneaker& s, int sneakerNumber)
{
    cout << "\nSneaker #" << sneakerNumber << endl;
    cout << "Model: " << s.model << endl;
    cout << "Brand: " << brandToString(s.brand) << endl;
    cout << "Size: " << s.size << endl;
    cout << "Condition: " << conditionToString(s.condition) << endl;
    cout << fixed << setprecision(2);
    cout << "Purchase Price: $" << s.purchasePrice << endl;
    cout << "Estimated Value: $" << s.estimatedValue << endl;
}

// ------------------------------------------------------------
// Main Program
// ------------------------------------------------------------
int main()
{
    // Part 4 - Create three Sneaker variables.
    Sneaker sneaker1;
    Sneaker sneaker2;
    Sneaker sneaker3;

    cout << "================================" << endl;
    cout << "   SNEAKER COLLECTION MANAGER" << endl;
    cout << "================================" << endl;

    // Part 5 - Enter information for each sneaker.
    sneaker1 = getSneakerInput(1);
    sneaker2 = getSneakerInput(2);
    sneaker3 = getSneakerInput(3);

    // Part 6 - Display the collection report.
    cout << "\n\n================================" << endl;
    cout << "      SNEAKER COLLECTION" << endl;
    cout << "================================" << endl;

    displaySneaker(sneaker1, 1);
    displaySneaker(sneaker2, 2);
    displaySneaker(sneaker3, 3);

    // Part 7 - Calculate the collection value.
    double totalPaid = sneaker1.purchasePrice + sneaker2.purchasePrice + sneaker3.purchasePrice;
    double totalValue = sneaker1.estimatedValue + sneaker2.estimatedValue + sneaker3.estimatedValue;
    double gainLoss = totalValue - totalPaid;

    cout << "\n================================" << endl;
    cout << "       COLLECTION SUMMARY" << endl;
    cout << "================================" << endl;
    cout << fixed << setprecision(2);
    cout << "Total Paid:       $" << totalPaid << endl;
    cout << "Current Value:    $" << totalValue << endl;
    cout << "Gain/Loss:        $" << gainLoss << endl;

    // Part 8 - Determine gain, loss, or no change.
    cout << endl;
    if (gainLoss > 0)
    {
        cout << "Your collection has increased in value!" << endl;
    }
    else if (gainLoss < 0)
    {
        cout << "Your collection has decreased in value." << endl;
    }
    else
    {
        cout << "Your collection value has stayed the same." << endl;
    }

    return 0;
}
