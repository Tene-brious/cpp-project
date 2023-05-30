#include <iostream>
#include <string>
#include <windows.h> // € symbol
#include <iomanip> // Necessary for setprecision

using namespace std;

// Global variables

string stock[3][4] = { {"Banana",     "200", "1.19", "0"},
                      {"Tangerine",  "150", "0.89", "0"},
                      {"Watermelon", "100", "1.99", "0"} };

string client[3][2] = { {"Banana",     "0"},
                       {"Tangerine",  "0"},
                       {"Watermelon", "0"} };

string vendas[10][3] = { {"Client Number", "Product Quantity", "Total Price"} };

int clientNumber = 1;
int totalProducts;

/**
 * Function to:
 * Reset cart values
 * Reset total products
 * Increment client number
 */
void resertAndUpdateValues() {
    for (int i = 0; i < 3; i++) {
        client[0][1] = "0";
    }

    totalProducts = 0;
    clientNumber++;
}

/**
 * Function for saving transactions
 * @param total
 */
void saveReceipts(float total) {

    if (clientNumber < 10) {
        vendas[clientNumber][0] = to_string(clientNumber);
        vendas[clientNumber][1] = to_string(totalProducts);
        vendas[clientNumber][2] = to_string(total);
    }
}

/**
 * Function to list the transactions
 */
void showListofReceipts() {
    for (int i = 0; i < 10; i++) {
        for (int j = 0; j < 3; j++) {
            cout << vendas[i][j];
            cout << "\t";
        }
        cout << "\n";
    }
    cout << "\n";

}

/**
 * Function that allows you to increase the stock
 */
void addStock() {
    int escolha;
    int quant;
    cout << "Choose the fruit(s) you want to add stock to: \n";
    cin >> escolha;
    switch (escolha) {
    case 1:
        cout << "Insert quantity: ";
        cin >> quant;
        stock[0][1] = to_string(stoi(stock[0][1]) + quant);
        break;
    case 2:
        cout << "Insert quantity: ";
        cin >> quant;
        stock[1][1] = to_string(stoi(stock[1][1]) + quant);
        break;
    case 3:
        cout << "Insert quantity: ";
        cin >> quant;
        stock[2][1] = to_string(stoi(stock[2][1]) + quant);
        break;
    }

}

/**
 * Function that allows you to see the current stock as well as the quantity of products already sold
 */
void relatoriostock() {
    for (int i = 0; i < 3; i++) {
        cout << "Current stock of " << stock[i][0] << ": " << stock[i][1] << "\n"; // nome do produto
        cout << "Stock that has been sold of " << stock[i][0] << ": " << stock[i][3] << "\n"; // stock vendido
    }
}

/**
 * Function to:
 * decrease stock
 * increase sold stock
 * increase quantity of products selected
 * calculation of total cost with and without iva
 * @param fruitPos
 */
void frutas(int fruitPos) { // new variable that identifies the fruit, buyout menu layout
    int quant;
    cout << "You have selected the " << stock[fruitPos][0] << "\n"; //
    cout << "\n" << "Price per unit: " << setprecision(4) << (stof(stock[fruitPos][2])) << "\n";
    cout << "\n" << "Quantity: ";
    cin >> quant;
    if (stoi(stock[fruitPos][1]) >= quant) {
        stock[fruitPos][1] = to_string(stoi(stock[fruitPos][1]) - quant); // updates initial stock
        stock[fruitPos][3] = to_string(stoi(stock[fruitPos][3]) + quant); // updates sold stock
        totalProducts += quant;
        cout << "Total price: " << (stof(stock[fruitPos][2]) * quant); // product calculation by the quantity that the client specified
        cout << "\n";

        client[fruitPos][1] = to_string(stoi(client[fruitPos][1]) + quant); //the line above's purpose is only to update the stock on the variable stock though we have to convert the quant (client inserted value)
    }
    else {
        cout << "We are sorry, we do not have such quantity \n";
        cout << "\n";
    }
}

/**
 * Function that calculates the iva price
 * @param price
 * @return
 */
float iva(float price) {
    return price * 0.23;
}

/**
 * Function for calculating the change
 * @param price
 * @return
 */
float troco(float price) {
    float valorpago;
    cout << "Insert payment value: ";
    cin >> valorpago;
    string valorPagoString = to_string(valorpago);
    if (valorpago < price) {
        cout << "Insufficient funds \n";
        troco(price);
    }
    else {
        return valorpago - price;
    }
}

/**
 * Function to show everything in the cart
 */
void checkout() {
    for (int i = 0; i < 3; i++) {
        if (client[i][0].compare("0")) {
            cout << "\n";
            cout << "Name: " << (client[i][0]) << "\n";
            cout << "Quantity: " << (client[i][1]) << "\n";
            cout << "Line number: " << i + 1 << "\n";
            cout << "Price without taxes(IVA): " << stoi(client[i][1]) * stof(stock[i][2]) << "\n";
        }
    }
}

/**
 * Function for printing the receipt details
 * @param nome
 */
void talao()
{
    if (totalProducts == 0) {
        cout << "You haven't selected any product";
        return;
    }

    string nome;
    cout << "Insert your name: ";
    cin >> nome;
    float total = stof(client[0][1]) * stof(stock[0][2]) + stof(client[1][1]) * stof(stock[1][2]) +
        stof(client[2][1]) * stof(stock[2][2]);
    cout << "Time to empty your cart \n";
    cout << "\n";
    cout << "Client's name: " << nome << "\n";
    cout << "Client number: " << clientNumber << "\n";
    checkout();
    cout << "\n";
    cout << "Total with taxes (iva): " << total + iva(total) << "\n";
    cout << "Your change sums up to: " << setprecision(2) << troco(total + iva(total));
    cout << "\n";

    saveReceipts((total + iva(total)));
}

void menu() {
    int escolha;
    do {
        cout << "				===================================================== \n";
        cout << " \t\t				   MENU DE COMPRA \t \n";
        cout << "				===================================================== \n";
        cout << "\n";
        cout << "						1.Bananas at 1.19/kg \n";
        cout << "						2.Tangerinas at 0.89/kg \n";
        cout << "						3.Melancia at 1.99/kg \n";
        cout << "						4.Checkout \n";
        cout << "						5.Finish your purchase  \n";
        cout << "						6.Stock Report \n";
        cout << "						7.Add Stock \n";
        cout << "						8.Show list of receipts \n";
        cout << "\n";


        cout << "Choose your fruit(s): \n";
        cout << "Option: ";
        cin >> escolha;
        cout << "\n";
        switch (escolha) {
        case 1:
            frutas(0);
            break;
        case 2:
            frutas(1);
            break;
        case 3:
            frutas(2);
            break;
        case 4:
            checkout();
            break;
        case 5:
            talao();
            resertAndUpdateValues();
            cout << "\n";
            break;
        case 6:
            relatoriostock();
            break;
        case 7:
            addStock();
            break;
        case 8:
            showListofReceipts();
            break;
        default:
            cout << "Invalid option \n";
            cout << "Choose another valid number to continue\n";
            cout << "\n";
            menu();
            break;
        }
    } while (escolha <= 8);
}

int main() {
    SetConsoleOutputCP(1252);
    menu();
}
