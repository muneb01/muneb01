#include <iostream>

using namespace std;

// Abstract Base Class
class Vehicle {
public:
    // Pure Virtual Function
    virtual void start() const = 0;

    // Non-virtual function
    void stop() const {
        cout << "Stopping the vehicle." << endl;
    }
};

// Concrete Derived Class: Car
class Car : public Vehicle {
public:
    // Implementation of the pure virtual function
    void start() const override {
        cout << "Starting the car engine." << endl;
    }
};

// Concrete Derived Class: Motorcycle
class Motorcycle : public Vehicle {
public:
    // Implementation of the pure virtual function
    void start() const override {
        cout << "Starting the motorcycle engine." << endl;
    }
};

// Concrete Derived Class: Truck
class Truck : public Vehicle {
public:
    // Implementation of the pure virtual function
    void start() const override {
        cout << "Starting the truck engine." << endl;
    }
};

int main() {
    // Create objects of the derived classes
    Car myCar;
    Motorcycle myMotorcycle;
    Truck myTruck;

    // Call the pure virtual function
    myCar.start();
    myMotorcycle.start();
    myTruck.start();

    // Call the non-virtual function
    myCar.stop();
    myMotorcycle.stop();
    myTruck.stop();

    return 0;
}



#include <iostream>
#include <string>

using namespace std;

class Product {
public:
    int productId;
    string productName;
    double price;

    Product(int id, const string& name, double cost)
        : productId(id), productName(name), price(cost) {}

    void displayProductDetails() {
        cout << "Product ID: " << productId << ", Name: " << productName << ", Price: $" << price << endl;
    }
};

class ShoppingCart {
private:
    Product* products;
    int itemCount;
    double totalCost;

public:
    ShoppingCart() : products(nullptr), itemCount(0), totalCost(0.0) {}

    void addProduct(const Product& product) {
        Product* newProducts = new Product[itemCount + 1];
        for (int i = 0; i < itemCount; ++i) {
            newProducts[i] = products[i];
        }
        newProducts[itemCount++] = product;

        delete[] products;
        products = newProducts;

        totalCost += product.price;
    }

    void displayAllProducts() {
        for (int i = 0; i < itemCount; ++i) {
            products[i].displayProductDetails();
        }
    }

    double calculateTotalCost() {
        return totalCost;
    }

    ~ShoppingCart() {
        delete[] products;
    }
};

class User {
public:
    int userId;
    ShoppingCart* cart;

    User(int id) : userId(id), cart(nullptr) {}

    void displayUserDetails() {
        cout << "User ID: " << userId << endl;
        if (cart != nullptr) {
            cout << "Shopping Cart Details:" << endl;
            cart->displayAllProducts();
            cout << "Total Cost: $" << cart->calculateTotalCost() << endl;
        } else {
            cout << "User does not have a shopping cart." << endl;
        }
    }

    ~User() {
        delete cart;
    }
};

int main() {
    Product laptop(1, "Laptop", 999.99);
    Product phone(2, "Smartphone", 499.99);

    User user1(101);
    user1.displayUserDetails();

    ShoppingCart cart1;
    cart1.addProduct(laptop);
    cart1.addProduct(phone);

    user1.cart = &cart1;
    user1.displayUserDetails();

    return 0;
}
