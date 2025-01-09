#include<iostream>
#include<vector>
#include<string>
#include<iomanip>
using namespace std;
enum TrafficLightState { RED, YELLOW, GREEN };
struct Vehicle
{
    int vehicleID;
    string ownerName;
    string vehicleType;
    string licensePlate;//hello
    string registrationDate;
};
struct Violation
{
    int violationID;
    int vehicleID;
    string violationType;
    string dateTime;
    double fineAmount;
};

vector<Vehicle> vehicles;
vector<Violation> violations;
vector<vector<string>> trafficDensity(3, vector<string>(3, "Low"));
void trafficLightSimulation()
{
    cout << "Traffic Light States Simulation:\n";
    TrafficLightState lights[] = { RED, YELLOW, GREEN };
    const char* states[] = { "RED", "YELLOW", "GREEN" };

    for (int intersection = 0; intersection < 3; ++intersection)
    {
        cout << "Intersection " << intersection + 1 << ": " << states[lights[intersection % 3]] << endl;
    }
    cout << "Traffic lights cycled successfully.\n";
}
void addVehicle()
{
    Vehicle v;
    cout << "Enter Vehicle ID: ";
    cin >> v.vehicleID;
    cin.ignore();
    cout << "Enter Owner Name: ";
    getline(cin, v.ownerName);
    cout << "Enter Vehicle Type: ";
    getline(cin, v.vehicleType);
    cout << "Enter License Plate: ";
    getline(cin, v.licensePlate);
    cout << "Enter Registration Date (YYYY-MM-DD): ";
    getline(cin, v.registrationDate);
    vehicles.push_back(v);
    cout << "Vehicle registered successfully.\n";
}
void displayVehicles()
{
    cout << "Registered Vehicles:\n";
    cout << "ID\tOwner Name\tType\tLicense Plate\tRegistration Date\n";
    for (const auto& v : vehicles)
    {
        cout << v.vehicleID << "\t" << v.ownerName << "\t" << v.vehicleType
             << "\t" << v.licensePlate << "\t" << v.registrationDate << endl;
    }
}
void recordViolation()
{
    Violation v;
    cout << "Enter Violation ID: ";
    cin >> v.violationID;
    cout << "Enter Vehicle ID: ";
    cin >> v.vehicleID;
    cin.ignore();
    cout << "Enter Violation Type: ";
    getline(cin, v.violationType);
    cout << "Enter Date and Time (YYYY-MM-DD HH:MM): ";
    getline(cin, v.dateTime);
    cout << "Enter Fine Amount: ";
    cin >> v.fineAmount;

    violations.push_back(v);
    cout << "Violation recorded successfully.\n";
}
void displayViolations()
{
    cout << "Recorded Traffic Violations:\n";
    cout << "ID\tVehicle ID\tType\t\tDate and Time\tFine\n";
    for (const auto& v : violations)
    {
        cout << v.violationID << "\t" << v.vehicleID << "\t" << v.violationType
             << "\t" << v.dateTime << "\t" << fixed << setprecision(2) << v.fineAmount << endl;
    }
}
void updateTrafficDensity()
{
    int intersection;
    string density;
    cout << "Enter Intersection (1-3): ";
    cin >> intersection;
    if (intersection < 1 || intersection > 3)
    {
        cout << "Invalid intersection number.\n";
        return;
    }
    cout << "Enter New Traffic Density (Low, Moderate, High): ";
    cin >> density;

    trafficDensity[intersection - 1][intersection - 1] = density;
    cout << "Traffic density updated successfully.\n";
}
void displayTrafficDensity()
{
    cout << "Traffic Density at Intersections:\n";
    for (int i = 0; i < 3; ++i)
    {
        cout << "Intersection " << i + 1 << ": " << trafficDensity[i][i] << endl;
    }
}
void adminDashboard()
{
    int choice;
    do {
        cout << "\nAdmin Dashboard:\n";
        cout << "1. Manage Traffic Lights\n";
        cout << "2. Register Vehicles\n";
        cout << "3. Record Traffic Violations\n";
        cout << "4. View Traffic Density\n";
        cout << "5. Update Traffic Density\n";
        cout << "6. Display Registered Vehicles\n";
        cout << "7. Display Violations\n";
        cout << "8. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice)
        {
            case 1:
                trafficLightSimulation();
                break;
            case 2:
                addVehicle();
                break;
            case 3:
                recordViolation();
                break;
            case 4:
                displayTrafficDensity();
                break;
            case 5:
                updateTrafficDensity();
                break;
            case 6:
                displayVehicles();
                break;
            case 7:
                displayViolations();
                break;
            case 8:
                cout << "Exiting Admin Dashboard.\n";
                break;
            default:
                cout << "Invalid choice. Try again.\n";
        }
    } while (choice != 8);
}
int main()
{
    cout << "Welcome to Smart City Traffic Management System\n";
    adminDashboard();
    return 0;
}


