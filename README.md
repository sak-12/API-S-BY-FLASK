# API-S-BY-FLASK
Here, I am creating an API for handling the backend part 
API 1:
 Endpoint : /API/total_items ,
API Use Cases :
1. Total item (total seats) sold in Marketing for last in q3 of the year?
Expected O/P: returns integer
Parameters: {start_date: DATE, end_date: DATE, department: string}

 CODE FOR THIS 
 from flask import Flask, request, jsonify

app = Flask(__name__)
dataset = ""C:\Users\PC\Downloads\data.csv"
@app.route('/api/total_items', methods=['GET'])
def get_total_items():
    start_date = request.args.get('start_date')
    end_date = request.args.get('end_date')
    department = request.args.get('department')

    total_quantity = 0

    for entry in the dataset:
        if start_date <= entry['date'] <= end_date and entry['department'] == department:
            total_quantity += entry['quantity']

    return jsonify(total_quantity)

if __name__ == '__main__':
    app.run()

API 2:
API Use Cases:
1. What is the 2nd most sold item in terms of quantity sold in q4,
2. What is the fourth most sold item in terms of Total price in q2?
Expected O/P: returns string name
Parameters: { item_by: ("quantity" | | "price"), start_date: DATE, end_date:

DATE, n: integer }

CODE :
def get_nth_most_total_item():
    item_by = request. args.get('item_by')
    start_date = request. args.get('start_date')
    end_date = request. args.get('end_date')
    n = int(request.args.get('n'))

    filtered_dataset = [entry for entry in dataset if start_date <= entry['date'] <= end_date]

    if item_by == 'quantity':
        sorted_items = sorted(filtered_dataset, key=lambda x: x['quantity'], reverse=True)
    elif item_by == 'price':
        sorted_items = sorted(filtered_dataset, key=lambda x: x['price'], reverse=True)
    else:
        return jsonify({"error": "Invalid value for 'item_by'. Must be 'quantity' or 'price'."})

    if n > len(sorted_items):
        return jsonify({"error": "Value of 'n' exceeds the number of items in the dataset."})

    nth_item = sorted_items[n - 1]['item']
    return jsonify(nth_item)

if __name__ == '__main__':
    app.run()

API 3:
API Use Cases:
1. What is the percentage of sold items (seats) department-wise?
Expected O/P: {dept_name: x%,....... }
Parameters: {start_date: Date, end_date: Date}

CODE:-
def get_percentage_of_department_wise_sold_items():
    start_date = request. args.get('start_date')
    end_date = request. args.get('end_date')

    filtered_dataset = [entry for entry in dataset if start_date <= entry['date'] <= end_date]

    department_total = {}
    total_quantity = 0

    for entry in filtered_dataset:
        department = entry['department']
        quantity = entry['quantity']

        if department not in department_total:
            department_total[department] = quantity
        else:
            department_total[department] += quantity

        total_quantity += quantity

    percentage_by_department = {}

    for department, quantity in department_total.items():
        percentage = (quantity / total_quantity) * 100
        percentage_by_department[department] = round(percentage, 2)

    return jsonify(percentage_by_department)

if __name__ == '__main__':
    app.run()

API 4:
Endpoint : /API/monthly_sales
API Use Cases:
1. How do the monthly sales for any product look like?
Expected O/P: [1908.0, … 1952.0] for all 12 months
Parameters: {product: String, year: Number}

CODE:
def get_monthly_sales():
    product = request. args.get('product')
    year = request. args.get('year')

    if product and year:
        if product in monthly_sales_data and year in monthly_sales_data[product]:
            monthly_sales = monthly_sales_data[product][year]
            return jsonify(monthly_sales)
        else:
            return jsonify(error="Invalid product or year"), 400
    else:
        return jsonify(error="Missing product or year"), 400

if __name__ == '__main__':
    app.run()




