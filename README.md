# SHOPPING-CART
/*
 Programmer: Jaiden Howard
 Project Name: Shopping Cart Part 4
 Date 12/4/2022
 Description: You must read the information from these files to be able to complete the program. 
 This information must be stored in a struct called Customer and Product. 
 You should have vectors of structures.update the program to allow one of the users to safely log in to their account, complete a maximum of 3 transactions, 
 and end the program. The updated values must be written to the file after each transaction.
 Item transactions should be added to the transactions.da file when a new purchase is made. 
 Three incorrect attempts at entering the username and password will end the program.
*/
#include <bits/stdc++.h>
using namespace std; 

    //=================================================
    // Variables
    //=================================================
    string sku,username,address,password,memberlevel,customername,yesorno;
    int quantity, option,attempts,choice;
    char answer;
    int t = 0;
    int i = 0;
    double newcredit, remainigstorecredit, price, rate;
    int currentaccount = i;
    
    
     struct Customer
    {
        string flname;
        string user; 
        string pass; 
        long account;
        string mlevel;
        double stcredit;
        string custaddress;    
    };

        struct Product
    {
        string SKU;
        string Name;	
        int Itemsinunit; 
        double Priceperunit;
        int QuantityonHand;
    };

    vector<Customer> accountinfo;
    vector<Product> productsinfo;
    int productsku = 0;
    double tax=0.06, discount=0;
    //=================================================
    
 //==============Case 5 – Log Out (exit/end the program)==============================
    int LogOut()
    { 
    cout<<endl<< "Log Out (exit/end the program)"<<endl;
    return 0;    
    }
//==============Case 4 – Update Account (update the user information)==============================
    void updateinfo()
    {
       ofstream updatedinfo("updatedaccountinfo.da");
        updatedinfo<<"";
        //==============Display Customer Account information===================
        //==============prompt user decide which parts of their account info they want to update=========

        cout<< "Customer account information"<<endl;
        cout << endl << "Customers Name: "<<accountinfo[currentaccount].flname<< endl;
        cout <<endl<<"Account: "<<accountinfo[currentaccount].account << endl;
        cout <<endl<<"Address: "<< accountinfo[currentaccount].custaddress<<endl;

        cout<<endl<<"Update Customer Name: Y or N"<<endl;
        cin>> yesorno;

        if(yesorno=="Y")
        {
            cout<<endl<<"Enter New Customer Name"<<endl;
            cin>>customername;
            accountinfo[currentaccount].flname=customername;
        }    
        
        cout<<endl<<"Update Password: Y or N"<<endl;
        cin>>yesorno;
        
        if (yesorno=="Y")
        {
            cout<<endl<<"Enter New Password"<<endl;
            cin >> password;
            accountinfo[currentaccount].pass=password;
        }
 
        cout<<endl<<"Update Customer Address: Y or N"<<endl;
        cin>>yesorno;
        
        if(yesorno=="Y")
        {
            cout<<endl<<"Update Customer Address: "<< endl;
            cin>> address;
            accountinfo[currentaccount].custaddress=address;
        }
        //==============Display Customer Account information===================

       
        cout << endl << "======================== Accout information ===============================";
        cout << endl << "Customers Name: "<<accountinfo[currentaccount].flname<< endl;
        cout <<"Account: "<< accountinfo[currentaccount].account << endl;
        cout<< "Member Level: "<< accountinfo[currentaccount].mlevel<<endl;
        cout <<"Address: "<< accountinfo[currentaccount].custaddress<<endl;
        cout<< "Remaining Store Credit: " << (accountinfo[currentaccount].stcredit)<<endl;

        updatedinfo<<accountinfo[currentaccount].flname<<","
        <<accountinfo[currentaccount].user<<","
        <<accountinfo[currentaccount].pass<<","
        <<accountinfo[currentaccount].account<<","
        <<accountinfo[currentaccount].mlevel<<","
        <<accountinfo[currentaccount].custaddress<< ","
        <<accountinfo[currentaccount].stcredit<<",";
        
    }
//==============Case 3 – Get an estimate (estimate the cost for purchasing an item)==============================
    void estimate()

    {
 
        //======= prompt uaer to input sku and quantity then calculate price and discount then apply discount===============
        cout<< "Enter sku: ";
        cin>>sku;
            if (sku == "HF-342")
        {   cout<<endl<<"Enter quantity: ";
            cin>>quantity;
            if (quantity<=200)
        {
            price=quantity * 20.00;
        }
        }
     
    
            else if(sku=="LK-322")
        {       cout<<endl<<"Enter quantity: ";
                cin>>quantity;
            if (quantity <= 76)
        {
            price=quantity * 5.75;
        }
        }
            else if (sku=="KF-231")
        {   cout<<endl<<"Enter quantity: ";
            cin>>quantity;
            if (quantity <=100)
        {
            price=quantity * 15.23;
        }
        }

            if (accountinfo[currentaccount].mlevel == "Gold" && price>= 300)
        {
            cout<<endl<<"8.5% Discount applied to purchase. "<<endl;
            discount = 0.085;
            price= price* (1-0.085);
             //==============Display Customer receipt=============

            cout << endl << "======================== Customer Reciept ===============================";
            cout << endl << "Customers Name: "<<accountinfo[currentaccount].flname<< endl;
            cout <<"Account: "<< accountinfo[currentaccount].account << endl;
            cout<< "Member Level: "<< accountinfo[currentaccount].mlevel<<endl;
            cout <<"Address: "<< accountinfo[currentaccount].custaddress<<endl;
            cout<< "Total Cost: "<<price<<endl;
            cout<< "Remaining Store Credit: " <<(remainigstorecredit=accountinfo[currentaccount].stcredit-price)<<endl;
            //==========================================================
            // Item Purchased
            //==========================================================
            if (sku == "HF-342")
                    {cout << "Purchased " << quantity << " 1/2 inch Bolts\n";}

            else if(sku=="LK-322")
                    {cout << "Purchased " << quantity << " 1/2 inch Nails\n";}

            else if (sku=="KF-231")
                    {cout << "Purchased " << quantity << " Hammers\n";}
            
            else if(sku=="RG-324")
                    {cout << endl<<"Purchased " << quantity << " 1/2 inch Screw\n";}

            else if (sku=="PL-643")
                    {cout <<endl<< "Purchased " << quantity << " Saw\n";}
            
            else if (sku=="PM-263")
                    {cout <<endl<< "Purchased " << quantity << " Lawn Mower\n";}

        //===========================================================
        //===========================================================    
        }
            else if (accountinfo[currentaccount].mlevel =="Gold" && price<300)
        {
            cout<<endl<<"6% Discount applied to purchase. "<<endl;
            discount = 0.06;
            price= price* (1-0.06);
        
            //==============Display Customer receipt=============
        
            cout << endl << "======================== Customer Reciept ===============================";
            cout << endl << "Customers Name: "<<accountinfo[currentaccount].flname<< endl;
            cout <<"Account: "<< accountinfo[currentaccount].account << endl;
            cout<< "Member Level: "<< accountinfo[currentaccount].mlevel<<endl;
            cout <<"Address: "<< accountinfo[currentaccount].custaddress<<endl;
            cout<< "Total Cost: "<<price<<endl;
            cout<< "Remaining Store Credit: " << (remainigstorecredit=accountinfo[currentaccount].stcredit - price)<<endl;
            //==========================================================
            // Item Purchased
            //==========================================================
            if (sku == "HF-342")
                    {cout << "Purchased " << quantity << " 1/2 inch Bolts\n";}

            else if(sku=="LK-322")
                    {cout << "Purchased " << quantity << " 1/2 inch Nails\n";}

            else if (sku=="KF-231")
                    {cout << "Purchased " << quantity << " Hammers\n";}
            
            else if(sku=="RG-324")
                    {cout << endl<<"Purchased " << quantity << " 1/2 inch Screw\n";}

            else if (sku=="PL-643")
                    {cout <<endl<< "Purchased " << quantity << " Saw\n";}
            
            else if (sku=="PM-263")
                    {cout <<endl<< "Purchased " << quantity << " Lawn Mower\n";}

            //===========================================================
            //===========================================================
        }
            else if (accountinfo[currentaccount].mlevel == "Blue" && price>= 100)
        {
            cout<<endl<<"6% Discount applied to purchase. "<<endl;
            discount = 0.06;
            price= price* (1-0.06);
            //==============Display Customer receipt=============
       
            cout << endl << "======================== Customer Reciept ===============================";
            cout << endl << "Customers Name: "<<accountinfo[currentaccount].flname<< endl;
            cout <<"Account: "<< accountinfo[currentaccount].account << endl;
            cout<< "Member Level: "<< accountinfo[currentaccount].mlevel<<endl;
            cout <<"Address: "<< accountinfo[currentaccount].custaddress<<endl;
            cout<< "Total Cost: "<<price<<endl;
            cout<< "Remaining Store Credit: " << (remainigstorecredit=accountinfo[currentaccount].stcredit-price)<<endl;
            //==========================================================
            // Item Purchased
            //==========================================================
            if (sku == "HF-342")
                    {cout << "Purchased " << quantity << " 1/2 inch Bolts\n";}

            else if(sku=="LK-322")
                    {cout << "Purchased " << quantity << " 1/2 inch Nails\n";}

            else if (sku=="KF-231")
                    {cout << "Purchased " << quantity << " Hammers\n";}
            
            else if(sku=="RG-324")
                    {cout << endl<<"Purchased " << quantity << " 1/2 inch Screw\n";}

            else if (sku=="PL-643")
                    {cout <<endl<< "Purchased " << quantity << " Saw\n";}
            
            else if (sku=="PM-263")
                    {cout <<endl<< "Purchased " << quantity << " Lawn Mower\n";}

            //===========================================================
            //===========================================================();
        
            price=price*(1+0.06);
        }
        
            else if (accountinfo[currentaccount].mlevel == "Diamond" && price>= 700)
        {
            cout<<endl<<"12% Discount applied to purchase. "<<endl;
            discount = 0.012;
            price= price* (1-0.012);
            //==============Display Customer receipt=============

            cout << endl << "======================== Customer Reciept ===============================";
            cout << endl << "Customers Name: "<<accountinfo[currentaccount].flname<< endl;
            cout <<"Account: "<< accountinfo[currentaccount].account << endl;
            cout<< "Member Level: "<< accountinfo[currentaccount].mlevel<<endl;
            cout <<"Address: "<< accountinfo[currentaccount].custaddress<<endl;
            cout<< "Total Cost: "<<price<<endl;
            cout<< "Remaining Store Credit: " << (remainigstorecredit=accountinfo[currentaccount].stcredit-price)<<endl;
            //==========================================================
            // Item Purchased
            //==========================================================
            if (sku == "HF-342")
                    {cout << "Purchased " << quantity << " 1/2 inch Bolts\n";}

            else if(sku=="LK-322")
                    {cout << "Purchased " << quantity << " 1/2 inch Nails\n";}

            else if (sku=="KF-231")
                    {cout << "Purchased " << quantity << " Hammers\n";}
            
            else if(sku=="RG-324")
                    {cout << endl<<"Purchased " << quantity << " 1/2 inch Screw\n";}

            else if (sku=="PL-643")
                    {cout <<endl<< "Purchased " << quantity << " Saw\n";}
            
            else if (sku=="PM-263")
                    {cout <<endl<< "Purchased " << quantity << " Lawn Mower\n";}

            //===========================================================
            //===========================================================();
        }

            else if (accountinfo[currentaccount].mlevel == "Diamond" && price< 700 && price>=300)
        {
            cout<<endl<<"8.5% Discount applied to purchase. "<<endl;
            discount = 0.085;
            price= price* (1-0.085);
            //==============Display Customer receipt=============

            cout << endl << "======================== Customer Reciept ===============================";
            cout << endl << "Customers Name: "<<accountinfo[currentaccount].flname<< endl;
            cout <<"Account: "<< accountinfo[currentaccount].account << endl;
            cout<< "Member Level: "<< accountinfo[currentaccount].mlevel<<endl;
            cout <<"Address: "<< accountinfo[currentaccount].custaddress<<endl;
            cout<< "Total Cost: "<<price<<endl;
            cout<< "Remaining Store Credit: " << (remainigstorecredit=accountinfo[currentaccount].stcredit-price)<<endl;
            //==========================================================
            // Item Purchased
            //==========================================================
            if (sku == "HF-342")
                    {cout << "Purchased " << quantity << " 1/2 inch Bolts\n";}

            else if(sku=="LK-322")
                    {cout << "Purchased " << quantity << " 1/2 inch Nails\n";}

            else if (sku=="KF-231")
                    {cout << "Purchased " << quantity << " Hammers\n";}
            
            else if(sku=="RG-324")
                    {cout << endl<<"Purchased " << quantity << " 1/2 inch Screw\n";}

            else if (sku=="PL-643")
                    {cout <<endl<< "Purchased " << quantity << " Saw\n";}
            
            else if (sku=="PM-263")
                    {cout <<endl<< "Purchased " << quantity << " Lawn Mower\n";}

            //===========================================================
            //===========================================================();
        }
            else if (accountinfo[currentaccount].mlevel =="Diamond" && price<300 && price>=100)
        {
            cout<<endl<<"6% Discount applied to purchase. "<<endl;
            discount = 0.06;
            price= price* (1-0.06);
            //==============Display Customer receipt=============

            cout << endl << "======================== Customer Reciept ===============================";
            cout << endl << "Customers Name: "<<accountinfo[currentaccount].flname<< endl;
            cout <<"Account: "<< accountinfo[currentaccount].account << endl;
            cout<< "Member Level: "<< accountinfo[currentaccount].mlevel<<endl;
            cout <<"Address: "<< accountinfo[currentaccount].custaddress<<endl;
            cout<< "Total Cost: "<<price<<endl;
            cout<< "Remaining Store Credit: " << (remainigstorecredit=accountinfo[currentaccount].stcredit-price)<<endl;
            //==========================================================
            // Item Purchased
            //==========================================================
            if (sku == "HF-342")
                    {cout << "Purchased " << quantity << " 1/2 inch Bolts\n";}

            else if(sku=="LK-322")
                    {cout << "Purchased " << quantity << " 1/2 inch Nails\n";}

            else if (sku=="KF-231")
                    {cout << "Purchased " << quantity << " Hammers\n";}
            
            else if(sku=="RG-324")
                    {cout << endl<<"Purchased " << quantity << " 1/2 inch Screw\n";}

            else if (sku=="PL-643")
                    {cout <<endl<< "Purchased " << quantity << " Saw\n";}
            
            else if (sku=="PM-263")
                    {cout <<endl<< "Purchased " << quantity << " Lawn Mower\n";}

            //===========================================================
            //===========================================================();
    
        
        } 
            else 
        {
        cout<<endl<<"6% Discount applied to purchase. "<<endl;
            discount = 0;
            price= price* (1-0.06);
            //==============Display Customer receipt=============

            cout << endl << "======================== Customer Reciept ===============================";
            cout << endl << "Customers Name: "<<accountinfo[currentaccount].flname<< endl;
            cout <<"Account: "<< accountinfo[currentaccount].account << endl;
            cout<< "Member Level: "<< accountinfo[currentaccount].mlevel<<endl;
            cout <<"Address: "<< accountinfo[currentaccount].custaddress<<endl;
            cout<< "Total Cost: "<<price<<endl;
            cout<< "Remaining Store Credit: " << (remainigstorecredit=accountinfo[currentaccount].stcredit-price)<<endl;
            //==========================================================
            // Item Purchased
            //==========================================================
            if (sku == "HF-342")
                    {cout << "Purchased " << quantity << " 1/2 inch Bolts\n";}

            else if(sku=="LK-322")
                    {cout << "Purchased " << quantity << " 1/2 inch Nails\n";}

            else if (sku=="KF-231")
                    {cout << "Purchased " << quantity << " Hammers\n";}
            
            else if(sku=="RG-324")
                    {cout << endl<<"Purchased " << quantity << " 1/2 inch Screw\n";}

            else if (sku=="PL-643")
                    {cout <<endl<< "Purchased " << quantity << " Saw\n";}
            
            else if (sku=="PM-263")
                    {cout <<endl<< "Purchased " << quantity << " Lawn Mower\n";}

            //===========================================================
            //===========================================================();
        }    
    
    }
        //===============Case 2 – View all items (list all items available)==============================
         void viewlist()
    {
        cout << endl << "    SKU      Name         Items in unit    Price per unit  Quantity" << endl;
        cout << "HF-342   1/2 in Bolt       50              20.00            200" << endl;
        cout << "RG-324   1/2 in Screw      30              20.00            174" << endl;
        cout << "LK-322   1/4 in nail       25               5.75             76" << endl;
        cout << "PL-643   Saw                1              35.67             35" << endl;
        cout << "PM-263   Lawn Mower         1             430.39             10" << endl;
        cout << "KF-231   Hammer             1              15.23            100"<< endl;
        
    }








       
int main()

{
    // open the transactions file that will store each transactions data//
    ofstream transactions("transactions.da");
    transactions<<"";

    // open the account iformation file and products file to read into the program//
    ifstream accountfile, products;
    string accountsvector, productsvector;

        accountfile.open("accounts-1.dat");

        for(int v = 0; v < 4; v++)
    {
        Customer tempcustomer;
        string _flname,_user,_pass,_acc,_mlevel,_stcredit,_cust;

        getline(accountfile, _flname, ';');
        tempcustomer.flname = _flname;

        getline(accountfile, _user, ';');
        tempcustomer.user = _user;

        getline(accountfile, _pass, ';');
        tempcustomer.pass = _pass;

        getline(accountfile, _acc, ';');
        tempcustomer.account = stoi(_acc);

        getline(accountfile, _mlevel, ';');
        tempcustomer.mlevel = _mlevel;

        getline(accountfile, _stcredit, ';');
        tempcustomer.stcredit = std::stod(_stcredit);

        getline(accountfile, _cust);
        tempcustomer.custaddress = _cust;
        accountinfo.push_back(tempcustomer);     
    }
        accountfile.close();
        remainigstorecredit=accountinfo[currentaccount].stcredit-price;

        products.open("products.csv");
        int itemsinunit[] = {};
        double priceperunit[] = {};
        for(int v = 0; v < 6; v++)
    {  
        Product temproduct;
        string _sku,_name,_its,_pu,_qh;
        getline(products, _sku, ',');
        temproduct.SKU = _sku;

        getline(products, _name, ',');
        temproduct.Name = _name;
        
        getline(products, _its, ',');
        temproduct.Itemsinunit = stoi(_its);

        getline(products, _pu, ',');
        temproduct.Priceperunit=priceperunit[v];

        getline(products, _qh);
       temproduct.QuantityonHand = stoi(_qh);

        productsinfo.push_back(temproduct);
    }
        products.close();
    
    
    attempts = 0;
    bool login = 0;//login was successful or not
    while (attempts<=2 && !login)
    {
    
        //prompt user to enter username and password, if invalid Display error message
        cout<< "Enter Username: "<<endl;
        cin>> username;

        cout<<endl<< "Enter Password: "<< endl;
        cin>> password;
        for (int i = 0; i <= 3; i++) 
        {
            if (username == accountinfo[i].user && password == accountinfo[i].pass)
            {
                cout<<"Login Complete"<<endl;
                currentaccount = i;

                login = 1;
                //============= Display Choice Table of items=================== 
                cout << endl << "    SKU      Name         Items in unit    Price per unit  Quantity" << endl;
                cout << "HF-342   1/2 in Bolt       50              20.00            200" << endl;
                cout << "RG-324   1/2 in Screw      30              20.00            174" << endl;
                cout << "LK-322   1/4 in nail       25               5.75             76" << endl;
                cout << "PL-643   Saw                1              35.67             35" << endl;
                cout << "PM-263   Lawn Mower         1             430.39             10" << endl;
                cout << "KF-231   Hammer             1              15.23            100 " << endl;
                break;
            }
        }
    
        if (!login){
            cout<< endl<<"Username or Password invalid"<< endl;
            attempts++;
        }
    }
        if (!login && attempts >= 3) 
        return 1;

        while (t <=3)
    {
        t+=1;
        if (t >=4)
           {
               return 1;
           }
            // Prompt user to make a selection from the choices listed 1-5
            cout<<endl<<"1 – Purchase an item (make a new purchase)"<<endl;
            cout<<endl<<"2 – View all items (list all items available)"<<endl;
            cout<<endl<<"3 – Get an estimate (estimate the cost for purchasing an item)"<<endl;
            cout<<endl<<"4 – Update Account (update the user information)"<<endl;
            cout<<endl<<"5 – Log Out (exit/end the program)"<<endl;
            cin>>option;

          //========Display sku options and prompt user to select one the enter preferred quantity========
            switch(option)   
        { 
            case 1: 
            {
           
            cout << endl<<"Enter 1 if you wish to purchase HF-342" << endl;
            cout << endl<<"Enter 2 if you wish to purchase RG-324"<<endl;
            cout << endl<<"Enter 3 if you wish to purchase LK-322"<<endl;
            cout << endl<<"Enter 4 if you wish to purchase PL-643"<< endl;
            cout << endl<<"Enter 5 if you wish to purchase PM-263"<<endl;
            cout << endl<<"Enter 6 if you wish to purchase KF-231"<<endl;
            
            cin >> choice;
            productsku=choice-1;

            switch(choice)
            {
                case 1:
                {
                sku = "HF-342";

                        cout<<endl<<"Enter quantity: ";
                        cin>>quantity;

                if (quantity<=200)
                    {
                        price=quantity * 20.00;

                    }
                        else
                    { 
                        cout << endl << " There are not enough products in our inventory to complete your transaction." << endl;

                        if(price>accountinfo[currentaccount].stcredit || price>remainigstorecredit)
                    {
                        cout<< endl<<"Error: Exceeding store credit."<<endl;
                    }
                        
                        price=price*(1+0.06);
                        t++;
                    }
              }  
                    break;

                    case 2:
                    {
                    sku = "RG-324";

                        cout<<endl<<"Enter quantity: ";
                        cin>>quantity;

                        if (quantity<=174)
                    {
                        price=quantity * 30.00;
                        
                    }
                        else
                    { 
                        cout << endl << " There are not enough products in our inventory to complete your transaction." << endl;

                        if(price>accountinfo[currentaccount].stcredit || price>remainigstorecredit)
                    {
                        cout<< endl<<"Error: Exceeding store credit."<<endl;
                    }
                        price=price*(1+0.06);
                    
                        t++;
                    }
                    }break;
            
                        case 3: 
                        {             
                        sku="LK-322";
                        cout<<endl<<"Enter quantity: ";
                        cin>>quantity;
                        if (quantity <= 76)
                    {
                        price=quantity * 5.75;
                    }
                        else 
                    {
                        cout << endl << " There are not enough products in our inventory to complete your transaction." << endl;
                
                        if(price>accountinfo[currentaccount].stcredit || price>remainigstorecredit)
                    {
                        cout<< endl<<"Error: Exceeding store credit."<<endl;
                    }
                        price=price*(1+0.06);
                       
                        t++;
                    }
                
                        }
                        break;

                        case 4:   
                        sku="PL-643";
                        cout<<endl<<"Enter quantity: ";
                        cin>>quantity;
                        if (quantity <=35)
                    {
                        price=quantity * 35.67;
                       
                    }
                        else 
                    {
                        cout << endl << " There are not enough products in our inventory to complete your transaction." << endl;
                        if(price>accountinfo[currentaccount].stcredit || price>remainigstorecredit)
                    {
                        cout<< endl<<"Error: Exceeding store credit."<<endl;
                    }
                        price=price*(1+0.06);
                      
                        t++;
                    }
                        break;

                        case 5:  
                        { 
                        sku="PM-263";
                        cout<<endl<<"Enter quantity: ";
                        cin>>quantity;
                        if (quantity <=100)
                    {
                        price=quantity * 430.39;
                      
                    }
                        else 
                    {
                        cout << endl << " There are not enough products in our inventory to complete your transaction." << endl;
                        if(price>accountinfo[currentaccount].stcredit || price>remainigstorecredit)
                    {
                        cout<< endl<<"Error: Exceeding store credit."<<endl;
                    }
                        price=price*(1+0.06);
                       
                        t++;
                    }
                        
                        }
                        break;
                
            
                        case 6:
                        {   
                        sku="KF-231";
                        cout<<endl<<"Enter quantity: ";
                        cin>>quantity;
                        if (quantity <=100)
                    {
                        price=quantity * 15.23;
                      
                    }
                        else 
                    {
                        cout << endl << " There are not enough products in our inventory to complete your transaction." << endl;
                        if(price>accountinfo[currentaccount].stcredit || price>remainigstorecredit)
                    {
                        cout<< endl<<"Error: Exceeding store credit."<<endl;
                    }
                        price=price*(1+0.06);
                     
                        t++;
                    }
                
                        }
                        break;
                    }
                    
                        if (t >= 4) 
                    {
                        //==============Display Customer receipt=============
                        cout << endl<<"======================== Customer Reciept ===============================";
                        cout << endl<<"Customers Name: "<<accountinfo[currentaccount].flname<< endl;
                        cout <<endl<<"Account: "<< accountinfo[currentaccount].account << endl;
                        cout<< endl<<"Member Level: "<< accountinfo[currentaccount].mlevel<<endl;
                        cout <<endl<<"Address: "<< accountinfo[currentaccount].custaddress<<endl;
                    
                        //==========================================================
                        // Item Purchased
                        //==========================================================
                        if (sku == "HF-342")
                        {cout << endl<<"Purchased " << quantity << " 1/2 inch Bolts\n";}

                        else if(sku=="LK-322")
                        {cout << endl<<"Purchased " << quantity << " 1/2 inch Nails\n";}

                        else if (sku=="KF-231")
                        {cout <<endl<< "Purchased " << quantity << " Hammers\n";}
                        else if(sku=="RG-324")
                        {cout << endl<<"Purchased " << quantity << " 1/2 inch Screw\n";}

                        else if (sku=="PL-643")
                        {cout <<endl<< "Purchased " << quantity << " Saw\n";}
                        else if (sku=="PM-263")
                        {cout <<endl<< "Purchased " << quantity << " Lawn Mower\n";}
                        //===========================================================
                        //===========================================================
                        break;
                
                    // calculate discount based on the users member level//
                    }
                        if (accountinfo[currentaccount].mlevel == "Gold" && price>= 300)
                        {
                            discount = 0.085;
                        }

                        else if (accountinfo[currentaccount].mlevel =="Gold" && price<300)
                        {
                            discount = 0.06;
                        }

                        else if (accountinfo[currentaccount].mlevel == "Blue" && price>= 100)
                        {
                            discount = 0.06;
                        }

                        else if (accountinfo[currentaccount].mlevel == "Diamond" && price>= 700)
                        {
                            discount=0.012;
                        }

                        else if (accountinfo[currentaccount].mlevel == "Diamond" && price< 700 && price>=300)
                        {
                            discount = 0.085;
                        }

                        else if (accountinfo[currentaccount].mlevel =="Diamond" && price<300 && price>=100)
                        {
                            discount = 0.06;
                        }

                        else
                        { discount=0;
                        }

                        productsinfo[productsku].QuantityonHand = quantity;
                        accountinfo[currentaccount].stcredit -= price;
                    // open the file containing account information to access login info then close the file
                        ofstream accFile;
                        accFile.open("accounts-1.dat");
                        for (int i = 0; i < 4; i++)
                        {
                            accFile << accountinfo[i].flname;
                            accFile << ';';
                            accFile << accountinfo[i].user;
                            accFile << ';';
                            accFile << accountinfo[i].pass;
                            accFile << ';';
                            accFile << accountinfo[i].account;
                            accFile << ';';
                            accFile << accountinfo[i].mlevel;
                            accFile << ';';
                            accFile << accountinfo[i].stcredit;
                            accFile << ';';
                            accFile << accountinfo[i].custaddress;
                            accFile << '\n';
                        }
                        accFile.close();
                    // open the file containing product information then close the file//
                        ofstream prodFile;
                        prodFile.open("products.csv");
                        for (int i = 0; i < 6; i++){
                            prodFile << productsinfo[i].SKU;
                            prodFile << ',';
                            prodFile << productsinfo[i].Name;
                            prodFile << ',';
                            prodFile << productsinfo[i].Itemsinunit;
                            prodFile << ',';
                            prodFile << productsinfo[i].Priceperunit;
                            prodFile << ',';
                            prodFile << productsinfo[i].QuantityonHand;
                            prodFile << '\n';
                        }
                        prodFile.close();

                        //==============Display Customer receipt=============
                       cout <<endl<<"======================== Customer Reciept ===============================";
                        cout <<endl<<"Customers Name: "<< accountinfo[currentaccount].flname<< endl;
                        cout <<endl<<"Account: "<< accountinfo[currentaccount].account << endl;
                        cout<< endl<<"Member Level: "<< accountinfo[currentaccount].mlevel<<endl;
                        cout <<endl<<"Address: "<< accountinfo[currentaccount].custaddress<<endl;
                        cout<< "Total Cost: "<<price<<endl;
                        cout<< "Remaining Store Credit: " <<(remainigstorecredit=accountinfo[currentaccount].stcredit-price)<<endl;
                        
                        // save the information from the transaction to the transactions.da file//
                        transactions<<accountinfo[currentaccount].flname<<","
                        <<accountinfo[currentaccount].account<<","
                        <<accountinfo[currentaccount].mlevel<<","
                        <<accountinfo[currentaccount].custaddress<< ","
                        <<accountinfo[currentaccount].stcredit<<","
                        <<productsinfo[productsku].SKU<<","
                        <<quantity<<","<<price<<","
                        <<discount<<","<<tax<<'\n';

                        //==========================================================
                        // Item Purchased
                        //==========================================================
                        if (sku == "HF-342")
                        {cout << endl<<"Purchased " << quantity << " 1/2 inch Bolts\n";}

                        else if(sku=="LK-322")
                        {cout << endl<<"Purchased " << quantity << " 1/2 inch Nails\n";}

                        else if (sku=="KF-231")
                        {cout << endl<<"Purchased " << quantity << " Hammers\n";}
                        else if(sku=="RG-324")
                        {cout << endl<<"Purchased " << quantity << " 1/2 inch Screw\n";}

                        else if (sku=="PL-643")
                        {cout <<endl<< "Purchased " << quantity << " Saw\n";}
                        else if (sku=="PM-263")
                        {cout <<endl<< "Purchased " << quantity << " Lawn Mower\n";}    
                        //===========================================================
                        //===========================================================
                        break;

                    }

                    
                        // ====== Case 2 view all items ================
        
                        case 2:  
                        viewlist();
                        break;

                        // ====== Case 3 get an estimate================
        
                        case 3:
                        estimate();
                        break;
        
                        //=========Case 4 update account info=================
        
        
                        case 4:
                        updateinfo();
                        break;

                        //=========Case 5 log out============================
                        case 5:
                        LogOut();
        
                        return 1;
                        break;
                    }
                }
    
                return 0;
}
