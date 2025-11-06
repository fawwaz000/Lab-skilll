#include <iostream>
#include <iomanip>
#include <string>
using namespace std;

double calcPartTimeSalary(double hours);
double calcPermanentSalary(double basic);

int main() {
    const int MAX = 100;
    string name[MAX], status[MAX];
    double basic[MAX], net[MAX];
    int n;
    
    cout << "=========================================\n";
    cout << "     WORKER NET SALARY CALCULATOR\n";
    cout << "=========================================\n";
    cout << "Enter number of workers: ";
    cin >> n;
    cout << endl;

    for (int i = 0; i < n; i++) {
        cout << "Worker " << i + 1 << " details:\n";
        cout << "Enter name: ";
        cin.ignore();
        getline(cin, name[i]);

        cout << "Enter status (part time / permanent): ";
        getline(cin, status[i]);

        if (status[i] == "part time" || status[i] == "Part time" || status[i] == "PART TIME") {
            double hours;
            cout << "Enter total working hours: ";
            cin >> hours;
            basic[i] = hours * 45.50;
            net[i] = calcPartTimeSalary(hours);
        } 
        else if (status[i] == "permanent" || status[i] == "Permanent" || status[i] == "PERMANENT") {
            cout << "Enter basic salary (must be above RM3000): RM ";
            cin >> basic[i];
            if (basic[i] < 3000) {
                cout << "Error: Basic salary must be above RM3000.\n";
                basic[i] = 3000; 
            }
            net[i] = calcPermanentSalary(basic[i]);
        } 
        else {
            cout << "Invalid status! Skipping...\n";
            basic[i] = net[i] = 0;
        }

        cout << endl;
    }

    cout << fixed << setprecision(2);
    cout << "=============================================================\n";
    cout << "                 WORKERS SALARY INFORMATION\n";
    cout << "=============================================================\n";
    cout << left << setw(20) << "Name"
         << setw(15) << "Status"
         << setw(15) << "Basic (RM)"
         << setw(15) << "Net Salary (RM)" << endl;
    cout << "-------------------------------------------------------------\n";

    for (int i = 0; i < n; i++) {
        cout << left << setw(20) << name[i]
             << setw(15) << status[i]
             << setw(15) << basic[i]
             << setw(15) << net[i] << endl;
    }

    cout << "=============================================================\n";
    return 0;
}

double calcPartTimeSalary(double hours) {
    double basic = hours * 45.50;
    double allowance = 0.10 * basic;
    return basic + allowance;
}

double calcPermanentSalary(double basic) {
    double allowance = 0.30 * basic;
    double epf = 0.15 * basic;
    return (basic + allowance) - epf;
}
