there are 8 kinds of events exists in our events.txt:
        format: use symbol " | "(| between two spaces) to cut each line of event into parts.

        for all events, if the employee's name("Zed"<manager>, "Olaf"<chef>, "Darius"<chef>, "Ashe"<server>, "Oriana"<server>) is wrong,
        system will print specified output in format like:
        "Invalid Employee name" +optional(for something (not somebody)).

        In our simulation, we only have 10 tables available.(table number 1 - 10)
        and if there is any input error, only error message will be generated and printed.
        if the event name is wrong, the system will prints "Invalid event name !"

    1."order": create an order, use the format to divided the event_line to six parts.
        first part(String): event name
            always "order"

        second part(String): server's name of the server who creates the order.
            Example: "Oriana" or "Ashe"(when instantiate the server in psvm, we crate the server's name)

        third part(String): the dish's name that the customs ordered.
            Example: "Sushi" (dish is Sushi)

        forth part(int): the table number of the table who make the order.
            Example: "1" (Table number 1)

        fifth part(String,int)or(String,int / String,int...): the addition of ingredients and quantity for this order.
            Use symbol " / "(/ between two spaces) to divided addition into parts. and each part divided by ","
            the string before the "," is the Ingredient name to add and the int after "," is the quantity of this Ingredient
            customs want to add. Symbol " / " will only used when there more than one Ingredient need to be added.
            If noting needs to add just write "N/A"
            Any addition will not change the price for the dish, the maximum addition quantity is 5 units.
            Example: "rice,1 / avocado,5" (add 1 unit rice and 5 units avocado to this order.)

        sixth part(String,int)or(String,int / String,int...): the subtraction of ingredients and quantity for this order.
            Use symbol " / "(/ between two spaces) to divided subtraction into parts. and each part divided by ","
            the string before the "," is the Ingredient name to subtract and the int after "," is the quantity of this Ingredient
            customs want to subtract. Symbol " / " will only used when there more than one Ingredient need to be subtract.
            If noting needs to subtract just write "N/A".
            Any subtraction will not change the price for the dish.
            Example: "wasabi,1" (subtract 1 unit wasabi)

        Example for order: "order | Ahri | Sushi | 1 | rice,1 / avocado,3 | wasabi,1"
            Table 1 orders a Sushi with addition of 1 unit rice and 3 units avocado and subtract 1 unit wasabi, the order is created by Ahri(Server)

        Error:  if the dish's name is not in the menu, system will print "Sorry, we don't have (wrong dish name)."
                if the addition or subtraction ingredients are not in the dish's recipe, system will print "(dish_name) does not have (subtract Ingredient name)"
                or print "(dish_name) can not add (add Ingredient name)"
                if the ingredients are not enough to cook this dish,system will prints "(chef name): Sorry, we ran out of Ingredient."

    2."seeOrder": the chef confirms the order.
        first part: event name
             always "seeOrder"

        second part(String): the chef's name of the chef who confirms the order.
            Example: "Olaf" or "Darius" (when instantiate the chef in psvm, we create the chef's name)

        third part(String): the dish's name of dish needed to be cooked.
            Example: "Sushi" (dish is Sushi)

        forth part(int): the table number of the order.
            Example: "1" (Table number 1)

        Example: "seeOrder | Olaf | Sushi | 1"
            Chef Olaf has confirm the order "Sushi" for table 1.

        Error:if the order name or table number is wrong, system will print "Sorry, Order (Wrong Order's name and table number) was never placed"


    3."fillOrder": the chef cook the order. Before cooking the order, the chef will check the dish in refrigerator, if it has same dish
                   chef will reheat it and use it again, if it doesn't have, then the chef will cook the order.
        first part: event name
             always "fillOrder"

        second part(String): the chef's name of the chef who cook the order.
            Example: "Olaf" or "Darius" (when instantiate the chef in psvm, we create the chef's name)

        third part(String): the dish's name of dish is cooked.
            Example: "Sushi" (dish is Sushi)

        forth part(int): the table number of the order.
            Example: "1" (Table number 1)
s
        Example: "fillOrder | Olaf | Sushi | 1"
            Chef Olaf has cooked the order "Sushi" for table 1.

        Error: if the order name or table number is wrong, system will print "Sorry, I didn't see (Wrong Order's and table number)"


    4."reject": when the server deliver the order to the table, the custom can reject the order by reasons.
        first part: event name
            always "reject"

        second part(String): the name of the server accept the reject.
            Example: "Oriana" or "Ashe"

        third part(String): the name of the Order customs want to reject.
            Example: "Sushi"

        forth part(int): table number of table reject the Order
            Example: "1"

        fifth part: always "N/A"

        sixth part: always "N/A"

        seventh part(String): the reason why customers reject the order.
            if the reason is "This dish is too cold" then the dish will reheat.
            if the reason is "The order is wrong" then the dish will be put into the refrigerator.
            if the reason is "This dish does not taste good" the this dish will be free.

        Example: "reject | Ahri | Mariated Ofu Soboro Mince | 1 | N/A | N/A | Dish is cold"
            Server Ahri accept the rejection of Order "Mariated Ofu Soboro Mince" in table 1 and send back to kitchen to reheat

        Error: if the order name or table number is wrong, system will print "Sorry, I didn't see (Wrong Order's and table number)"
               if the reason why customers reject the order is wrong, system will print "Invalid reject reason !".
               if the employee name is wrong, system will print
                  "Invalid Employee name for getting the reject with reheat reason.(not a Server)"
               or "Invalid Employee name for getting the reject with wrong order.(not a Server)"
               or "Invalid Employee name for getting the reject with taste reason.(not a Server)"

    5."deliver": the server deliver the dish to the table and accept by the custom
        first part: event name
            always "deliver"

        second part(String): name of the server who deliver the order.
            Example: "Oriana" or "Ashe"

        third part(String)the name of the Order customs accept.
            Example: "Mabo Tofu"

        forth part(int): table number of table accept the Order
            Example: "1"

        Example: "deliver | Ashe | Mabo Tofu | 2"
            Server Ashe has delivered the "Mabo Tofu" to table 2

        Error:if the order name or table number is wrong, system will print "Sorry, no such order to deliver."

    6."getBill": the server shows the details of the bill and calculate the total price. After getting bill, the table
                 will be cleaned.
        first part: event name
            always "getBill"

        second part(String): name of the server who take the bill.
            Example: "Oriana" or "Ashe"

        third part: always "N/A"

        forth part(int): table number of table wants to take the bill
            Example: "1"

        Example: "getBill | Oriana | N/A | 1"
            Server Oriana print the bill for table 1.

        Error: if the table number is wrong, system will print "Oops, table (Wrong table number) have not ordered anything yet."


    7."setRequest": the manager set the request for specific amount of an Ingredient
        first part: event name
            always "setRequest"

        second part(String): name of the manager who set the request.
            Example: "Zed" (when instantiate the manager in psvm, we crate the manager's name)

        third part(String): the name of ingredients needed request.
            Example: "soy milk"

        forth part(int):  quantity of the Ingredient the manager wants to request
            Example: "100"

        Example: "setRequest | Zed | soy milk | 100"
            Manager Zed wants to request 100 units of "soy milk".

        Error:if there is no such Ingredient exist in Ingredient.txt, system will prints "This name of Ingredient is wrong."
              if this Ingredient does not call request, system will prints "This Ingredient does not call request."



    8."receive" the employee receive the requested ingredients and move to the inventory.
        first part: event name
            always "receive"

        second part(String): name of the employee who receive the ingredients.
            Example: "Ashe" or "Olaf" or "Zed"(any employee of the restaurant)

        third part: the name of ingredients needed request.
            Example: "soy milk"

        forth part:  quantity of the ingredients that receive

        Example: "receive | Ashe | N/A | 0"
                  Ingredients have been received by employee Ahri.

    9."checkInventory" the manager can prints all the ingredients and quantity in the inventory.
        first part: event name
            always "checkInventory"

        second part(String): the name of the manager.
            Example: "Zed"

        third part: always "N/A"

        forth part: always "0"

        Example: "checkInventory | Zed | N/A | 0" Zed is checking the inventory and prints all the ingredients and quantities.

        Error: if this is not a Manager who wants to check inventory, system will print "Invalid Employee name for setting request.(not a Manager)"