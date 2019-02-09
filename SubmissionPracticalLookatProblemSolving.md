# **Exercises**
# **Questions**

### **1. Help!  Customers are not getting their products from the following assembly line.**

`// Prototype for a product
 var Product = {
   isPackaged: false,
   isLoaded: false,
   color: "uncolored",
   paint: function (color) {
     // The Painting Station will paint the product the desired color.
     console.log("Painting product " + color + ".");
     this.color = color;
     console.log("Product painted " + color + ".");
   },
   package: function (shippingType) {
     // The Packaging Station will package the product for the shipping type specified.
     // E.g. Next Day Shipping
     console.log("Packaging product for " + shippingType + ".");
     this.shippingType = shippingType;
     this.isPackaged = true;
     console.log("Product packaged for " + shippingType + ".");
   },
   loadOnTruck: function () {
     // The Loading Station will load the product on a truck to be shipped
     // to the customer.
     console.log("Loading product onto truck.");
     this.isLoaded = true;
     console.log("Product loaded onto the truck.");
   }
 };

 var order = function (color, shippingType) {
   // Creation Station: basic product is created.

   // Object.create will create a new object that has Product as
   // the prototype of that object. This means that any property lookups
   // performed will look first at the instance and then at Product.
   var product = Object.create(Product);

   console.log("Basic product created.");

   // Painting Station: product is painted.
   product.paint(color);

   // Packaging Station: product is packaged to be shipped.
   product.package(shippingType);

   // Loading Station: product is loaded onto a truck.
   product.loadOnTruck;

   return product;
 };`

 The output you see is:

    "Basic product created."

    "Painting product black."

    "Product painted black."

    "Packaging product for Next Day."

    "Product packaged for Next Day."

 Based on this output how would you figure out what the problem is?
 Identify the line(s) that are broken.

 Well this was a little bit tricky as there wasn't an error generated but there were a number of steps in the process that were begun and finished. The part of the manufacturing process where things broke down was between the "Product packaged for Next Day." and the Loading Station where we should see "Loading product onto truck."

 In looking at the Loading Station Code I found a syntax error ... it reads "product.loadOnTruck;" this is incorrect ... the correct code is "product.loadonTruck();" once this is correct I get an additional two console.log messages ...

 "Loading product onto truck."
 and 
 "Product loaded onto the truck."

 ### **2. Help!  Another assembly line is broken.**

  ```
  // Prototype for a product
 var Product = {
   isPackaged: false,
   isLoaded: false,
   color: "uncolored",
   paint: function (color) {
     // The Painting Station will paint the product the desired color.
     console.log("Painting product " + color + ".");
     this.color = color;
     console.log("Product painted " + color + ".");
   },
   package: function (shippingType) {
     // The Packaging Station will package the product for the shipping type specified.
     // E.g. Next Day Shipping
     console.log("Packaging product for " + shippingType + ".");
     this.shippingType = shippingType;
     this.isPackaged = true;
     console.log("Product packaged for " + shippingType + ".");
   },
   loadOnTruck: function () {
     // The Loading Station will load the product on a truck to be shipped
     // to the customer.
     console.log("Loading product onto truck.");
     this.isLoaded = true;
     console.log("Product loaded onto the truck.");
   }
 };

 var order = function (color, shippingType) {
   // Creation Station: basic product is created.

   // Object.create will create a new object that has Product as
   // the prototype of that object. This means that any property lookups
   // performed will look first at the instance and then at Product.
   var product = Object.create(Product);

   console.log("Basic product created.");

   // Painting Station: product is painted.
   product.paint(color);

   // Packaging Station: product is packaged to be shipped.
   product.package();

   // Loading Station: product is loaded onto a truck.
   product.loadOnTruck();

   return product;
 };
 ```

 The output you see is;

    "Basic product created."

    "Painting product black"

    "Product painted black."

    "Packaging product for undefined." ... very good we have shippingType showing up as undefined ... we will zero in on this in a bit ...

    "Product packaged for undefined." ... very good same error with shippingType showing up as undefined ..

    "Loading product onto truck."

    "Product loaded onto the truck."

    So the step and code we need to inspect is the code around the packaging station ...

    I found the following syntax error ... product.package();

    Packaging should be defined by the type of packaging but here it is blank ...

    The correction is product.package(shippingType)

 After I made that correction ... 

    "Packaging product for Next Day Air."

    and

    "Product packaged for Next Day Air."

    It now works ... yea!


