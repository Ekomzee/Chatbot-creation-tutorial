# 🤖 Amazon Lex Chatbot – Bank Account Assistant  

This project builds a **banking chatbot** using **Amazon Lex** and **AWS Lambda** to check account balances, manage user data, and handle multiple account types.  

## 📌 Features  
✅ Create an **Intent** in Amazon Lex  
✅ Manage **Fallback Intent**  
✅ Add **Custom Slots for Account Types**  
✅ Create a **Check Balance Intent**  
✅ Set up an **AWS Lambda Function**  
✅ Connect Lambda with Amazon Lex  
✅ Save **User Information**  
✅ Create a **Follow-Up Check Balance Intent**  
✅ Build a **Chatbot with Multiple Slots**  

---

## 🚀 Step-by-Step Guide  

### **1️⃣ Create an Amazon Lex Chatbot**  
1. Go to **Amazon Lex Console** and create a new bot.  
2. Choose **"Create a new intent"** and name it `CheckBalanceIntent`.  

### **2️⃣ Add Slots (Custom User Inputs)**  
- Create a **slot** for account type:  
  - Name: `accountType`  
  - Slot type: **Custom (Savings, Checking, Business)**  

### **3️⃣ Manage Fallback Intent**  
- Enable the **Fallback Intent** to handle unexpected inputs.  

### **4️⃣ Create AWS Lambda Function**  
- Open **AWS Lambda** and create a function.  
- Use **Python** and write a function to check account balance.  

```python
import json

def lambda_handler(event, context):
    account_type = event['sessionState']['intent']['slots']['accountType']['value']['interpretedValue']
    
    # Example account balances
    balances = {
        "savings": "$5,000",
        "checking": "$2,000",
        "business": "$10,000"
    }
    
    balance = balances.get(account_type.lower(), "Account type not found")
    
    response = {
        "sessionState": {
            "dialogAction": {"type": "Close"},
            "intent": {"name": "CheckBalanceIntent", "state": "Fulfilled"}
        },
        "messages": [{"contentType": "PlainText", "content": f"Your {account_type} balance is {balance}."}]
    }
    
    return response


