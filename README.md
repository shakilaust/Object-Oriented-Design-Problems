# Object Oriented Design

### Design a Library Management System

##### Use Cases

1. Any library member should be able to search books by their title, author, subject category as well by the publication date.

2. Each book will have a unique identification number and other details including a rack number which will help to physically locate the book.

3. There could be more than one copy of a book, and library members should be able to check-out and reserve any copy. We will call each copy of a book, a book item.

4. The system should be able to retrieve information like who took a particular book or what are the books checked-out by a specific library member.

5. There should be a maximum limit (5) on how many books a member can check-out.

6. There should be a maximum limit (10) on how many days a member can keep a book.

7. The system should be able to collect fines for books returned after the due date.

8. Members should be able to reserve books that are not currently available.

9. The system should be able to send notifications whenever the reserved books become available, as well as when the book is not returned within the due date.

10. Each book and member card will have a unique barcode. The system will be able to read barcodes from books and members’ library cards.

We have three main actors in our system:

- Librarian: Mainly responsible for adding and modifying books, book items, and users. The Librarian can also issue, reserve, and return book items.

- Member: All members can search the catalog, as well as check-out, reserve, renew, and return a book.

- System: Mainly responsible for sending notifications for overdue books, canceled reservations, etc.


Here are the main classes of our Library Management System:




### PakingLot Design

### Use Cases
1. The parking lot has multiple Parking Spots
2. The Parking lot can park motorcycles, cars and buses. 
3. The Parking lot has the motorcycle Spots, Compact Spots and large Spots
4. Each ParkingSpot is contain with number and Type. Type is either SMALL or Regular
5. To park a motorCycle we need any free spot.
6. To park a car we need any free Regular Spot. 
7. To park a bus we need consecutive 5 regular Spot


```cpp

enum VehicleSize {  MOTORCYCLE, COMPACT, LARGE };
enum ParkingSpotType { SMALL, REGULAR };

class ParkingSpot {

    private:
        int number;
        bool isFree;
        ParkingSpotType type;

    public:
        ParkingSpot( int number, ParkingSpotType type){
            isFree = true;
            number = number;
            type = type;
        }

        bool isParkingSportFree() {
            return isFree;
        }

        int getNumber() {
            return number;
        }

        int getType() {
            return type;
        }

        void makeParkingSpotBooked() {
            isFree = false;
        }

};


class Vehicle {

    private:
        vector < ParkingSpot > parkingSpots;   // FOr bus we need 5 consecutive spot
        string licensePlate;

    protected:
        VehicleSize size;
        int spotNeeded;

    public:
        Vehicle( string licenceNumber) {
            licensePlate = licenceNumber;
        }
        int getSpotNeeded() {
            return spotNeeded;
        }

        int getVehicleSize() {
            return size;
        }

        void clearSpot() {
            parkingSpots.clear();
        }

        void addParkingSport(ParkingSpot p) {
            parkingSpots.push_back(p);
        }

        virtual bool canVehicleFitIntoSpot( ParkingSpot s ) = 0;

};

class Car: public Vehicle {


    Car(string licensePlate): Vehicle(licensePlate) {
        size = COMPACT;
        spotNeeded = 1;
    }

    bool canVehicleFitIntoSpot(  ParkingSpot s ) {
        if(  s.isParkingSportFree() && s.getType() == REGULAR ) {
            return true;
        } else return false;
    }
};

class MotorCycle: public Vehicle {


    MotorCycle(string licensePlate): Vehicle(licensePlate) {
        size = COMPACT;
        spotNeeded = 1;
    }

    bool canVehicleFitIntoSpot(  ParkingSpot s ) {
        if( s.isParkingSportFree()  ) {
            return true;
        } else return false;
    }
};


class Bus: public Vehicle {

     Bus(string licensePlate): Vehicle(licensePlate) {
        size = COMPACT;
        spotNeeded = 5;
    }

    bool canVehicleFitIntoSpot(  ParkingSpot s ) {
        if( s.isParkingSportFree() && s.getType() == REGULAR  ) {
            return true;
        } else return false;
    }

    // Assuming that 5 consecutive Spots are given
    bool canBusFitIntoSpot( vector < ParkingSpot > s ) {
        for( int i = 0 ; i < s.size() ; i++ ) {
            if( !canVehicleFitIntoSpot(s[i])) {
                return false;
            }

        }
        return true;

    }


};



class ParkingLot {

    private:
        vector < ParkingSpot > parkingspots;

    public:

        ParkingLot(vector < ParkingSpot > p) {
            parkingspots = p;

        }

        vector <ParkingSpot> getFreeParkingSpots() {
            vector < ParkingSpot > results;
            for( int i = 0 ; i < parkingspots.size() ; i++ ) {
                if( parkingspots[i].isParkingSportFree()) {
                    results.push_back(parkingspots[i]);
                }
            }

            return results;

        }


};

```


### Online Shopping System ( Amazon, Flipcart ) 

Major Entities

1. Customer 
2. Cart ( One Cart of each Customer )
3. Product
4. Item ( Product, Quantity ) 
5. Order 
6. Shipping
7. Notification

```
enum AccountStatus { ACTIVE, INACTIVE };
enum OrderStatus { UNSHIPED, PENDING, SHIPPED, COMPLETED, CANCELED };

class ProductCategory {
private:
    string name, description;

};


class Account {
    private:
        string username, password, name, email, phone;
        AccountStatus status;
    public:

};

class Item {

    private:
        string productId;
        double price;
        int quantity;
    public:
        Item(string productId, double price, int quantity) {
            this->productId = productId;
            this->price = price;
            this->quantity = quantity;
        }

        string getProductId() {
            return productId;
        }

        double getPrice() {
            return price;
        }

        int getQuantity() {
            return quantity;
        }

        void setQuantity(int quantity) {
            quantity = quantity;
        }

};


class ShopingCart{
    private:
        vector < Item > items;
    public:
        ShopingCart() {
        }

        void addItem(Item a) {
            items.push_back(a);
        }

        void removeItem( Item a ) {

           // items.erase(a);
        }

        vector<Item> getItems() {
            return items;
        }


};

class Shipment{ 
    string shipmentNumber;
    
}

class Order{
private:
    string OrderNumber;
    OrderNumber status;
};



class Customer {

    Account account;
    ShopingCart cart;
    Order order;

public:
    void addItemToCart(Item a) { }
    void removeItemFromCart( Item a ) { }
    void placedOrder(Order ord) {}



};


class Product {

    private:
        string productId, name, description;
        double price;
        ProductCategory category;
        int avaiableItemCount;
        Account seller;
    public:
        Product(string productId, string name, string description, double price, int avaiableItemCount, ProductCategory ctg, Account seller) {
            productId = productId;
            name = name;
            description = description;
            price = price;
            category = ctg;
            seller = seller;


        }

        string getProductId() {
            return productId;
        }

        double getPrice() {
            return price;
        }

        void setPrice(double price) {
            price = price;
        }

        int getAvailableItemCount() {
            return avaiableItemCount;
        }

        void setAvailableItemCount( int avaiableItemCount) {
            avaiableItemCount = avaiableItemCount;
        }

};


```