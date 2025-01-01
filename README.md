#include <iostream>
#include <fstream>
#include <string>
#include <iomanip>
#include <conio.h>

using namespace std;

struct Flight
 {
    string flightNumber;
    string destination;
    string departureTime;
    string duration;
    float price;
};

struct Customer 
{
    int customerId;
    string name;
    int age;
    string gender;
    string address;
    string phone;
};

void inputCustomerDetails(Customer& customer) 
{     
    system("cls");
     cout<<"\n\n\n\n\n\n\n";
     cout<<"\t\t\t\t\t\t\t<--------------- CUSTOMER DETAILS FORM --------------->\n\n";
    cout<<"\t\t\t\t\t\t\tEnter Customer ID: ";
    cin>>customer.customerId;
    cin.ignore();
    cout<<"\t\t\t\t\t\t\tEnter Name: ";
    getline(cin, customer.name);
    cout<<"\t\t\t\t\t\t\tEnter Age: ";
    cin>>customer.age;
    cin.ignore();
    cout<<"\t\t\t\t\t\t\tEnter Gender: ";
    getline(cin, customer.gender);
    cout<<"\t\t\t\t\t\t\tEnter Address: ";
    getline(cin, customer.address);
    cout<<"\t\t\t\t\t\t\tEnter Phone Number: ";
    getline(cin, customer.phone);
    cout<<"\n";
    cout<<"\t\t\t\t\t\t\tCustomer details saved successfully!"<<endl;
    cout<<"\n\n";
    system("pause");
}

void printTicket(int customerId, const Customer& customer, const Flight& flight) 
{   
    system("cls");
    ofstream outf("ticket.txt");
    if (outf.is_open())
	 {
        outf<<"<------------ Airline Ticket ------------>\n";
        outf<<"Customer ID:    \t"<<customer.customerId << endl;
        outf<<"Customer Name:  \t"<<customer.name<<endl;
        outf<<"Customer Gender:\t"<<customer.gender<<endl;
        outf<<"Flight Number:  \t"<<flight.flightNumber<<endl;
        outf<<"Destination:    \t"<<flight.destination<<endl;
        outf<<"Departure Time: \t"<<flight.departureTime<<endl;
        outf<<"Duration:       \t"<<flight.duration << " hours" <<endl;
        outf<<"Price:          \t Rs."<<flight.price<<endl;
    }
    outf.close();
    cout<<"\n\n\n\n\n\n\n";
    cout << "\t\t\t\t\t\t\tTicket has been printed! Check 'ticket.txt'.\n";

}

void displayTicket(int customerId, const Customer& customer, const Flight& flight) 
{        
    system("cls");
	cout<<"\n\n\n\n\n\n\n"<<endl;
    cout<<"\t\t\t\t\t\t\t <------------ Airline Ticket ------------>\n";
    cout<<"\t\t\t\t\t\t\t Customer ID:        "<<customer.customerId<<endl;
    cout<<"\t\t\t\t\t\t\t Customer Name:     "<<customer.name<<endl;
    cout<<"\t\t\t\t\t\t\t Customer Gender:    "<<customer.gender<<endl;
    cout<<"\t\t\t\t\t\t\t Flight Number:      "<<flight.flightNumber<<endl;
    cout<<"\t\t\t\t\t\t\t Destination:        "<<flight.destination<<endl;
    cout<<"\t\t\t\t\t\t\t Departure Time:     "<<flight.departureTime<<endl;
    cout<<"\t\t\t\t\t\t\t Duration:           "<<flight.duration<<" hours"<<endl;
    cout<<"\t\t\t\t\t\t\t Price:             Rs."<<flight.price<<endl;
}

 void bookAndAddDetails(Customer& customer, Flight flights[], int flightCount, int& ticketId, bool& flightBooked, Flight& selectedFlight)
 {
 	    system("cls");
                  flights[0] = {"Pk-498", "  Dubai", "08-12-2024 7:40PM", " 04", 14000 }; 
                  flights[1] = {"Pk-198", "  Canada", "22-01-2024 5:40AM", " 16", 34000 };
                  flights[2] = {"Pk-798", "  UK", "09-12-2024 7:40PM", " 14", 44000 }; 
                  flights[3] = {"Pk-578", "  USA", "25-02-2024 5:40AM", " 18", 94000 }; 
                  flights[4] = {"Pk-898", "  Australia", "22-01-2024 5:40AM", " 16", 64000 }; 
                  flights[5] = {"Pk-348", "  Europe", "22-01-2024 5:40AM", " 07", 78000 }; 
                  flightCount = 6; 

     cout<<"\n\n\n\n\n\n\n";
    cout<<left<<setw(20)<<"\t\t\tFlight No"<<setw(10)<<" \tDestination"
   <<setw(20)<<"\t\t   Departure"<<setw(10)<<"\t Duration"
      <<"       Price"<<endl; 
    for (int i=0;i<flightCount;++i) 
     { 
            cout<<left<<setw(10)<<"\t\t"
			<<flights[i].flightNumber 
            <<setw(15)<<"\t"<<flights[i].destination 
			<<setw(20)<<"\t"<<flights[i].departureTime 
           <<"\t"<<flights[i].duration<<setw(10)<<" hours" 
       <<"\t"  <<"Rs."<< flights[i].price << endl;
    }

 cout<<"\n\t\t\t\t\t\t\tSelect a flight by entering the flight number: ";
 
         string selectedFlightNumber; 
        cin>>selectedFlightNumber; 
         bool flightFound = false; 
for(int i = 0; i < flightCount; ++i)
 {
      if(flights[i].flightNumber == selectedFlightNumber)
      { 
            selectedFlight = flights[i]; 
			flightFound = true; 
			flightBooked = true;
	       break; 
      }
 }
 if(flightFound) 
      {
           cout<<"\n\t\t\t\t\t\t\tEnter Customer Details:\n\n";
               inputCustomerDetails(customer); 
             cout<<"\n\t\t\t\t\t\t\tFlight booked successfully!\n";
            displayTicket(ticketId++, customer, selectedFlight);
      }
      else
        { 
                cout<<"\n\t\t\t\t\t\t\tInvalid flight number! Please try again.\n";
        }
        system("pause");
}


void printBookedTicket(int ticketId, bool flightBooked, const Customer& customer, const Flight& selectedFlight)
 { 
    system("cls");
      if (flightBooked) 
    {
       cout<<"\n"; 
       printTicket(ticketId - 1, customer, selectedFlight);
    } 
       else 
    { 
       cout<<"\n\n\n\n\n\n\n\t\t\t\t\t\t\tNo ticket has been booked yet.\n"; 
    }
    system("pause");
 }

void aboutUs()
 {
    system("cls");
    cout << "\n\n\n\n\n\n\n"
     << "\t\t\t\t\t<-------------------------------- About Us ------------------------------->\n"
     << "\n\t\t\t\t\tWelcome to Hazel Blue Airline where we believe that every journey is more\n"
     << "\t\t\t\t\tthan just reaching a destination. Your safety, connection, and comfort\n"
     << "\t\t\t\t\tare our priorities. We believe that aviation is proof that with\n"
     << "\t\t\t\t\tdetermination, we have the capacity to achieve the impossible.\n"
     << "\n\t\t\t\t\tThis airline was founded by four members whose names are given below:\n"
     << "\t\t\t\t\tAhmad, Saqib, Ali, and Rehman, with a passion for aviation and excellence.\n"
     << "\t\t\t\t\tTogether, we navigate the skies with ease and comfort, creating unforgettable\n"
     << "\t\t\t\t\tjourneys with you.\n"
     << "\n\t\t\t\t\t<------------------------------------------------------------------------>\n";

//    cout<<"\n\n\n\n\n"
//        <<"\t\t\t\t\t\t\t<-------------------------------- About Us ------------------------------->\n"
//        <<"\n\t\t\t\t\t\tWelcome to Hazel Blue Airline where we believe that every journey is more \n"
//        <<"\t\t\t\t\t\t\t than just reaching a destination Your safety, connection and comfort \n"
//        <<"\t\t\t\t\t\t\tis our priority. Our airline also believe that aviation is proof that with "
//        <<"\n\t\t\t\tdetermination we have the capacity to achieve the impossible.\n"
//        <<"\n\t\t\t\t\t\tThis airline was founded by four members whose names are given below: \n"
//        <<"\t\t\t\t\t\t Ahmad, Saqib, Ukasha and Unbreen with a passion for aviation and excellence. \n"
//        <<"\t\t\t\t\tTogether we navigate the skies with ease and comfort and create unforgettable journey with you people.\n"
//        <<"\n\t\t\t\t\t\t<---------------------------------------------------------------------->\n";
       system("pause");
    }
        
        
void mainMenu()
 {

   int choice;
   int ticketId = 8989; 
   Customer customer; 
   Flight flights[10];
    int flightCount = 0; 
//	initializeAndDisplayFlights(flights, flightCount); 
	Flight selectedFlight;
	 bool flightBooked = false;
    do 
	{
     system("cls");
        cout<<"\n\n\n\n\n\n\n                 " << endl;
        cout<<"\t\t\t\t\t\t\t<---------- WELCOME TO OUR AIRLINE ---------->\n" << endl;
//        cout<<"\t\t\t\t\t\t\t\t  [1] View Available Flights             " << endl;
        cout<<"\t\t\t\t\t\t\t\t  [1] Book a Flight                      " << endl;
        cout<<"\t\t\t\t\t\t\t\t  [2] Print Ticket                       " << endl;
        cout<<"\t\t\t\t\t\t\t\t  [3] What We Are?                       " << endl;
        cout<<"\t\t\t\t\t\t\t\t  [4] Exit                               " << endl;
       cout<<"\n";
        cout<<"Enter your choice: ";
        cin>>choice;
        cout<<"\n";

        switch(choice) 
		{
//          case 1:
//        	{
//			
////        	  cout<<"\t\t\t\t\t\t\tAvailable Flights:\n\n";
////               initializeAndDisplayFlights (flights, flightCount);
//            }
//            break;
          
          case 1:
		    {    
		    bookAndAddDetails(customer,  flights,  flightCount,  ticketId, flightBooked,  selectedFlight);
		     }
            break;
       
        case 2:
        	{
           printBookedTicket( ticketId, flightBooked,  customer,  selectedFlight);
           	}
            break;
       case 3:
       	  {
       		aboutUs();
		   }
            	
            	break;
            	
        case 4:
        	{
        		cout<<"\t\t\t\t\t\t\tThank you for using Hazel Blue  Airline!\n";
			}
            
            break;
        default:
        {
        	 cout<<"\n\t\t\t\t\t\t\tInvalid choice! Please try again.\n";
		}
		system("pause");
           
        }
        
        
    } while(choice != 4);
}


int main()
 {
 	  
    system("color F0"); 
    cout<<"\n\n\n\n";
//cout<<"\t\t\t\t\t\t\t          Hazel Blue Airline   \n\n"<<endl; 
    mainMenu();
    
    return 0;
}
