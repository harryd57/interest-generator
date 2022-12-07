#include<iostream>
#include<fstream>
//Author: Group SIX
//The program below is to print amount due to 50 investors in a bank after a time period of 6 months.
//Out of the 50 investors, 25 invested in treasury bills with an interest rate of 20%.
//Another 25 invested in fixed deposit with an interest rate of 10%.
using namespace std;
//The function 'interest' takes a single parameter principal, which is the sum invested.
//It calculates the interest made after a period of 6 months with an interest rate of 20%.
//It is for the treasury bills  investment.
double interest(double principal){
    //Using the formula to calculate simple interest which is principal x rate/100 x time in years.
    //In the below expression the interest rate of 20% is divided by 100, which equals 0.2.
    //The time period of 6 months is divided by 12 months, since 12 months = 1 year and time is in years. The result is 0.5 years.
    double rate = 0.2 ,time = 0.5;
    double answer = principal * rate * time;
    return answer;
}

//The function 'inteRest' takes a single parameter principal, which is the sum invested.
//It calculates the interest made after a period of 6 months with an interest rate of 10%.
//It is for the Fixed deposit investment.
double inteRest(double principal){
    //Using the formula to calculate simple interest which is principal x rate/100 x time in years.
    //In the below expression the interest rate of 10% is divided by 100, which equals 0.1.
    //The time period of 6 months is divided by 12 months, since 12 months = 1 year and time is in years. The result is 0.5 years.
    double rate = 0.1 ,time = 0.5;
    double answer = principal * rate * time;
    return answer;
}
//The 'welcome' function displays a welcome message and prompts the user to enter an investment section.
void welcome(){
    cout <<"Welcome to Ruby Bank!"<<endl;
    cout <<"Enter t to invest in the treasury bills section or f to invest in the fixed deposit section."<<endl;
    cout <<"Enter d to skip this session."<<endl;
    cout <<"Enter a command: ";
}
int main()
{
    string fName, lName, section;
    double principal, inTerest, amount;
    welcome();
    cin >> section;
    cout << " " <<endl;
    if (section == "t"){
      ofstream outFile;
      outFile.open("treasury bills.csv", ios::app);
      cout << "Enter your first name: ";
      cin >> fName;
      cout <<  "Enter your last name: ";
      cin >> lName;
      cout << "How much do you want to invest?: ";
      cin >> principal;
      inTerest = interest(principal);
      amount = principal + inTerest;
      outFile<< fName <<"," << lName << "," << principal <<","<< inTerest<< ","<<amount<< endl;
      outFile.close();
    }else if (section == "f"){
        ofstream outFile;
        outFile.open("fixed deposits.csv", ios::app);
        cout << "Enter is your first name: ";
        cin >> fName;
        cout <<  "Enter your last name: ";
        cin >> lName;
        cout << "How much do you want to invest?: ";
        cin >> principal;
        inTerest = inteRest(principal);
        amount = principal + inTerest;
        outFile<< fName <<"," << lName << "," << principal <<","<< inTerest<< ","<<amount<< endl;
        outFile.close();
    }
    cout << " " <<endl;
    cout << "Enter t to view the treasury bills section or f to view the fixed deposits section: ";
    cin >> section;
    if (section == "t"){
        ifstream inFile("treasury bills.csv");
        if(!inFile.is_open()){
            cout << "ERROR: File open"<<endl;
        }
        string fName;
        string lName;
        string principal;
        string inTerest;
        string amount;
        while(inFile.good()){

            getline(inFile,fName,',');
            getline(inFile,lName,',');
            getline(inFile,principal,',');
            getline(inFile,inTerest,',');
            getline(inFile,amount,'\n');

            cout << "Name: "<<fName<< " "<<lName<<endl;
            cout << "Invested: $"<<principal<<endl;
            cout << "Interest: $"<<inTerest<<endl;
            cout << "Total Amount: $"<<amount<<endl;
            cout <<".........................."<<endl;
        }
        inFile.close();
    }else if(section == "f"){
          ifstream inFile("fixed deposits.csv");
        if(!inFile.is_open()){
            cout << "ERROR: File open"<<endl;
        }
        string fName;
        string lName;
        string principal;
        string inTerest;
        string amount;
        while(inFile.good()){

            getline(inFile,fName,',');
            getline(inFile,lName,',');
            getline(inFile,principal,',');
            getline(inFile,inTerest,',');
            getline(inFile,amount,'\n');

            cout << "Name: "<<fName<< " "<<lName<<endl;
            cout << "Invested: $"<<principal<<endl;
            cout << "Interest: $"<<inTerest<<endl;
            cout << "Total Amount: $"<<amount<<endl;
            cout <<".........................."<<endl;
            
        }
        inFile.close();
    }

}
