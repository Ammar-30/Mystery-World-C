#include <iostream>
#include <vector>
#include <cstdlib>
#include <ctime>
using namespace std;

// Entity class (Base class)
class Entity {
public:
    virtual char Symbol() const = 0;
    virtual void move() = 0;
    virtual void displayInfo() const = 0;
    virtual ~Entity() {}
};

// Inanimate entities: Stone and Hole
class Stone : public Entity {
public:
    char Symbol() const override {
        return 'S';
    }
    void move() override {}
    void displayInfo() const override {
        cout << "Type: Stone" << endl;
    }
};

class Hole : public Entity {
private:
    int depth;
public:
    Hole(int d) : depth(d) {}
    char Symbol() const override {
        return 'O';
    }
    void move() override {}
    void displayInfo() const override {
        cout << "Type: Hole" << endl;
        cout << "Depth: " << depth << endl;
    }
};

// Animate entities: Human, Dragon, Monster
class Human : public Entity {
private:
    string name;
    int health;
    int positionX;
    int positionY;
public:
    Human(const string n) : name(n), health(100) {
        positionX = 0;
        positionY = 0;
    }
    char Symbol() const override {
        return '@';
    }
    void move() override {
        // Move to the right if possible, otherwise move randomly
        if (positionY < 9) {
            positionY++;
        } else {
            int direction = rand() % 4;
            switch (direction) {
                case 0: // Up
                    if (positionX > 0) {
                        positionX--;
                    }
                    break;
                case 1: // Down
                    if (positionX < 9) {
                        positionX++;
                    }
                    break;
                case 2: // Left
                    if (positionY > 0) {
                        positionY--;
                    }
                    break;
                case 3: // Right
                    if (positionY < 9) {
                        positionY++;
                    }
                    break;
            }
        }
        health--;
    }
    void displayInfo() const override {
        cout << "Type: Human" << endl;
        cout << "Name: " << name << endl;
        cout << "Health: " << health << endl;
    }
};

class Dragon : public Entity {
private:
    int health;
    int positionX;
    int positionY;
public:
    Dragon() : health(100) {
        positionX = 0;
        positionY = 0;
    }
    char Symbol() const override {
        return '#';
    }
    void move() override {
        // Move randomly to an unoccupied adjacent cell
        int direction = rand() % 4;
        switch (direction) {
            case 0: // Up
                if (positionX > 0) {
                    positionX--;
                }
                break;
            case 1: // Down
                if (positionX < 9) {
                    positionX++;
                }
                break;
            case 2: // Left
                if (positionY > 0) {
                    positionY--;
                }
                break;
            case 3: // Right
                if (positionY < 9) {
                    positionY++;
                }
                break;
        }
        health = health - rand() % 6; // Reducing health by a random number between 0 and 5
    }
    void displayInfo() const override {
        cout << "Type: Dragon" << endl;
        cout << "Health: " << health << endl;
    }
};

class Monster : public Entity {
private:
    int strength;
    int health;
    int positionX;
    int positionY;
public:
    Monster(int s) : strength(s), health(100) {
        positionX = 0;
        positionY = 0;
    }
    char Symbol() const override {
        return '*';
    }
    void move() override {
        // Move as many cells as its strength allows
        int direction = rand() % 4;
        switch (direction) {
            case 0: // Up
                for (int i = 0; i < strength; i++) {
                    if (positionX > 0) {
                        positionX--;
                    } else {
                        break;
                    }
                }
                break;
            case 1: // Down
                for (int i = 0; i < strength; i++) {
                    if (positionX < 9) {
                        positionX++;
                    } else {
                        break;
                    }
                }
                break;
            case 2: // Left
                for (int i = 0; i < strength; i++) {
                    if (positionY > 0) {
                        positionY--;
                    } else {
                        break;
                    }
                }
                break;
            case 3: // Right
                for (int i = 0; i < strength; i++) {
                    if (positionY < 9) {
                        positionY++;
                    } else {
                        break;
                    }
                }
                break;
        }
        health = health - strength; // Reduce health by the strength value
    }
    void displayInfo() const override {
        cout << "Type: Monster" << endl;
        cout << "Strength: " << strength << endl;
        cout << "Health: " << health <<endl;
    }
};

// Room class
class Room {
private:
    vector<vector<Entity*>> grid;
public:
    Room() {
        // Initialize the grid with empty cells
        grid.resize(10, vector<Entity*>(10, nullptr));
    }

    void displayRoom() const {
        for (int i = 0; i < 10; i++) {
            for (int j = 0; j < 10; j++) {
                if (grid[i][j] == nullptr) {
                    cout << ". ";
                } else {
                    cout << grid[i][j]->Symbol() << ' ';
                }
            }
            cout << endl;
        }
    }

    void displayEntityInfo(int row, int col) const {
        if (grid[row][col] != nullptr) {
            grid[row][col]->displayInfo();
        } else {
            cout << "No entity at this position (" << row << ", " << col << ")" << endl;
        }
    
    }
    void resetRoom() {
        // Clean up the entities
        for (int i = 0; i < 10; i++) {
            for (int j = 0; j < 10; j++) {
                if (grid[i][j] != nullptr) {
                    delete grid[i][j];
                    grid[i][j] = nullptr;
                }
            }
        }
        // Add new entities randomly
        srand(time(0));
        for (int i = 0; i < 2; i++) {
            int row = rand() % 10;
            int col = rand() % 10;
            if (grid[row][col] == nullptr) {
                grid[row][col] = new Stone();
            } else {
                i--;
            }
        }
        for (int i = 0; i < 2; i++) {
            int row = rand() % 10;
            int col = rand() % 10;
            if (grid[row][col] == nullptr) {
                int depth = rand() % 21;
                grid[row][col] = new Hole(depth);
            } else {
                i--;
            }
        }
        for (int i = 0; i < 3; i++) {
            int row = rand() % 10;
            int col = rand() % 10;
            if (grid[row][col] == nullptr) {
                string name;
                switch (i) {
                    case 0:
                        name = "Harold";
                        break;
                    case 1:
                        name = "David";
                        break;
                    case 2:
                        name = "Clare";
                        break;
                }
                grid[row][col] = new Human(name);
            } else {
                i--;
            }
        }
        for (int i = 0; i < 3; i++) {
            int row = rand() % 10;
            int col = rand() % 10;
            if (grid[row][col] == nullptr) {
                grid[row][col] = new Monster(rand() % 6);
            } else {
                i--;
            }
        }
        for (int i = 0; i < 2; i++) {
            int row = rand() % 10;
            int col = rand() % 10;
            if (grid[row][col] == nullptr) {
                grid[row][col] = new Dragon();
            } else {
                i--;
            }
        }
    }
};

// Main class
class Main {
private:
    Room room;
public:
    void startGame() {
        room.resetRoom();

        int choice;
        do {
            cout << "Menu:" << endl;
            cout << "1. Display Room" << endl;
            cout << "2. Move all entities" << endl;
            cout << "3. Display entity state by coordinates" << endl;
            cout << "4. Reset the room" << endl;
            cout << "5. Finish" << endl;
            cout << "Enter your choice: ";
            cin >> choice;

            switch (choice) {
                case 1:
                    room.displayRoom();
                    break;
                case 2:
                    room.resetRoom();
                    room.displayRoom();
                    cout << "Entities moved." << endl;
                    break;
                case 3:
                    int row, col;
                    cout << "Enter the row(0-9): ";
                    cin >> row;
                    cout << "Enter the column(0-9): ";
                    cin >> col;
                    room.displayEntityInfo(row, col);
                    break;
                case 4:
                    room.resetRoom();
                    cout << "Room reset." << endl;
                    break;
                case 5:
                    cout << "Game ended." << endl;
                    break;
                default:
                    cout << "Invalid choice." << endl;
            }
        } while (choice != 5);
    }
};
int main() {
    Main game;
    game.startGame();
    return 0;
}

