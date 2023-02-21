# Hotel-Management
#include <iostream>
#include <fstream>
#include <string>
#include <stdio.h>
#include <time.h>

const int NUM_SECONDS = 10;
using namespace std;
int total_amount = 0;
int pepsi = 5;
int sprite = 5;
int water = 5;
int burger = 5;
int pizza = 5;
int chips = 5;
int food_profit = 0;

void rooms(){
    cout << "Select the option (1-3): " << endl;
    cout << "(1) Book a room" << endl;
    cout << "(2) Room's availability" << endl;
    cout << "(3) Go to main menu" << endl;
    int x;
    cin >> x;
    if(x == 1){
        string name,surname;
        cout << "Enter room's number: ";cin >> x; cout << endl;
        cout << "Enter your name: "; cin >> name; cout << endl;
        cout << "Enter your surname: "; cin >> surname; cout << endl;
        fstream file;
        file.open(to_string(x) + ".txt",ios::out);
        file << name << endl;
        file << surname << endl;
        file.close();
        cout << "Room booked successfully" << endl;
        total_amount += 50;
    }
    else if(x == 2){
        cout << "Enter room's number: "; cin >> x; cout << endl;
        ifstream file;
        file.open(to_string(x) + ".txt");
        if(!file){
            return;
        }
        string s;
        file >> s;
        if(s == ""){
            cout << "Room is available" << endl;
        }
        else {
            cout << "Room is not available" << endl;
            cout << "It is booked by " << s << " ";
            file >> s;
            cout << s;
            cout << endl;
        }
        file.close();
    }
    else if(x == 3){
        return;
    }
}
void food_drinks(){
    int x;
    cout << "Select option (1-2): " << endl;
    cout << "(1) Food" << endl;
    cout << "(2) Drinks" << endl;
    cin >> x;cout << endl;
    if(x == 1){
        cout << "Select option (1-3): " << endl;
        cout << "(1) Burger - 5tg" << endl;
        cout << "(2) Chips - 2tg" << endl;
        cout << "(3) Pizza - 7tg" << endl;
        cin >> x;cout << endl;
        if(x == 1){
            if(burger == 0){
                cout << "Not left" << endl;
                food_drinks();
            }
            total_amount += 5;
            food_profit += 5;
            burger -= 1;
        }
        else if(x == 2){
            if(chips == 0){
                cout << "Not left" << endl;
                food_drinks();
            }
            total_amount += 2;
            food_profit += 2;
            chips -= 1;
        }
        else if(x == 3){
            if(pizza == 0){
                cout << "Not left" << endl;
                food_drinks();
            }
            total_amount += 7;
            food_profit += 7;
            pizza -= 1;
        }
    }
    else if(x == 2){
        cout << "Select option (1-3): " << endl;
        cout << "(1) Sprite - 5tg" << endl;
        cout << "(2) Water - 2tg" << endl;
        cout << "(3) Pepsi - 7tg" << endl;
        cin >> x;cout << endl;
        if(x == 1){
            if(sprite == 0){
                cout << "Not left" << endl;
                food_drinks();
            }
            total_amount += 5;
            food_profit += 5;
            sprite -= 1;
        }
        else if(x == 2){
            if(water == 0){
                cout << "Not left" << endl;
                food_drinks();
            }
            total_amount += 2;
            food_profit += 2;
            water -= 1;
        }
        else if(x == 3){
            if(pepsi == 0){
                cout << "Not left" << endl;
                food_drinks();
            }
            total_amount += 7;
            food_profit += 7;
            pepsi -= 1;
        }
    }
}
void total(){
    cout << "Select the option(1-3)" << endl;
    cout << "(1) Total amount of food and drinks left" << endl;
    cout << "(2) Earned amount of money from sold food" << endl;
    cout << "(3) Total earned money from the day" << endl;
    int x;
    cin >> x;cout << endl;
    if(x == 1){
        cout << "Burger: " << burger << endl;
        cout << "Chips: " << chips << endl;
        cout << "Pizza: " << pizza << endl;
        cout << "Pepsi: " << pepsi << endl;
        cout << "Water: " << water << endl;
        cout << "Sprite: " << sprite << endl;
    }
    else if(x == 2){
        cout << "Earned money from food: " << food_profit << endl;
    }
    else if(x == 3){
        cout << "Total money earned all combined: " << total_amount << endl;
    }
}
void code(int count){
    cout << "Select the option (1-4): " << endl;
    cout << "(1) Rooms" << endl;
    cout << "(2) Food and Drinks" << endl;
    cout << "(3) Total sales and collections" << endl;
    cout << "(4) Exit" << endl;
    cout << "(5) Total earned monet everyday" << endl;
    int x;
    cin >> x;
    if(x == 1){
        rooms();
        code(count);
    }
    else if(x == 2){
        food_drinks();
        code(count);
    }
    else if(x == 3){
        total();
        code(count);
    }
    else if(x == 4){
        string s = "Day ";
        s += to_string(count);
        s += ':';
        s += to_string(total_amount);
        fstream file;
        file.open("Total.txt",ios::in);
        fstream file5;
        file5.open("temp.txt",ios::out);
        string d;
        string add;
        int i = 1;
        while(file >> d){
            file5 << d << endl;
            i = i + 1;
        }
        file5 << s << endl;
        file5.close();
        file.close();
        ofstream n("Total.txt");
        n.close();
        fstream f;
        f.open("temp.txt",ios::in);
        fstream F;
        F.open("Total.txt",ios::out);
        string r;
        string c;
        i = 1;
        while(f >> r){
            F << r << endl;
            i = i + 1;
        }
        f.close();
        F.close();
        ofstream m("temp.txt");
        m.close();
        return;
    }
    else if(x == 5){
        fstream file;
        file.open("Total.txt",ios::in);
        string s;
        int i = 1;
        while(file >> s){
            if(i%2 == 1){
                cout << s << " ";
            }
            else{
                cout << s;
                cout << endl;
            }
            i = i + 1;
        }
        code(count);
    }
}
int main(){
    int count = 0;

    double time_counter = 0;

    clock_t this_time = clock();
    clock_t last_time = this_time;

    printf("Gran = %ld\n", NUM_SECONDS * CLOCKS_PER_SEC);

    while(true)
    {
        this_time = clock();

        time_counter += (double)(this_time - last_time);

        last_time = this_time;

        if(time_counter > (double)(NUM_SECONDS * CLOCKS_PER_SEC))
        {
            time_counter -= (double)(NUM_SECONDS * CLOCKS_PER_SEC);
            printf("%d\n", count);
            total_amount = 0;
            food_profit = 0;
            burger = 5;
            chips = 5;
            pizza = 5;
            pepsi = 5;
            sprite = 5;
            water = 5;
            count++;
            ofstream file1("1.txt");
            file1.close();
            ofstream file2("2.txt");
            file2.close();
            ofstream file3("3.txt");
            file3.close();
            code(count);
        }

        printf("DebugTime = %f\n", time_counter);
    }
    return 0;
}
