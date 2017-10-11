### Table of Contents

- [Introduction](#introduction)
- [Data Sets](#data-sets)
- [Learning Resources](#learning-resources)
- [Calculated Fields](#calculated-fields)

### Introduction
Visual analytics is an iterative and interactive
approach to analytical reasoning that transforms data into knowledge in BI applications. Visual analytics results are commonly shown in interactive, easy-to-use dashboards, that show most import information at a single glance.

In this demo, we'll look at sales data of a global sales that distributes furniture, office supplies, and technology products to consumers, corporate clients, and home offices.

The situation is as follows: <br>
The executives of the Global SuperStore–a global store specialized in office supplies, furnitures, and technology products–invited the board of directors and regional managers for a meeting next month to discuss the company's recent performances and discuss the company's future direction.

You are now being hired as a BA task force to the executives with a executive dashboards and reports that

1. inform on global and regional performance patterns
2. identify most and least profitable products in the various regions


### Data Sets

- [Global SuperStore 2016](https://goo.gl/1v3MkF) or [here on GitHub](https://goo.gl/J7Kd8L)
- [Tableau Sample Data](https://public.tableau.com/en-us/s/resources)

### Learning Resources

- [10 commonly used visualization types by Sisense](https://goo.gl/gGwoz1)
- [Tableau online learning resources](https://goo.gl/iyny4o)
- [Best practices in dashboard design by Tableau](https://goo.gl/QLG7M2)
- [Ryan Sleeper's visualization tutorials](https://www.ryansleeper.com)
- [Interworks Tableau training](https://goo.gl/6KH9ik)



_More to be added soon._

### Calculated Fields

- Profit ratio expresses the profitability of a product. Of my sales revenue, which percentage turns into profits. We can calculate it on the total sales and profits, or on each order individually.

  ```
  Profit Ratio (%) =
     SUM([Profit]) / SUM([Sales])
  ```

  ```
  Profit Ratio By Order =
     [Profit] / [Sales]
  ```

  ```
  IF RANK((-1)*(SUM([Profit]))) <= 5
      THEN "#"+ STR(RANK(ABS(SUM([Profit]))) ) + " " + MIN([City])
  ELSE ""
  END
  ```

We can calculat potential profits for _simulated scenarios_.

- Profits after removing discounts in the sales.
  ```
  Potential Profit (No Discount for LPC) =
     IF [Low Performing Countries in AP]
     THEN [Profit] + [Discount]/100 * [Sales]
     ELSE [Profit]
     END
  ```
- Profits after removing costs of shipping products.

  ```
  Potential Profit (Free Shipping for LPC) =
     IF [Low Performing Countries in AP]
     THEN [Profit] + [Shipping Costs]
     ELSE [Profit]
     END
  ```
- Profits after adding discounts back in and removing shipping costs.
  ```
  Potential Profit (No Discount + Free Shipping for LPC)  =
     IF [Low Performing Countries in AP]
     THEN [Profit] + [Shipping Cost] + [Discount]/100 * [Sales]
     ELSE [Profit]
     END
  ```

- Profits after a price increase. (Price Increase needs to be a defined parameter.)
  ```
  Potential Profit after Price Increase =
     IF [Low Performing Countries in AP]
     THEN [Potential Profit (No Discount + Free Shipping for LPC) ] + [Sales] * [Price Increase]
     ELSE [Profit]
     END
  ```

- New profits ratios can also be calculated.
  ```
  New Profit Ratio (%) =
     SUM([Potential Profit after Price Increase]) / SUM([Sales])
  ```
