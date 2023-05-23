# Geek Brains. Объектно-ориентированное программирование (семинары). ООП: Solid
домашнее задание 6

Объектно-ориентированное программирование (семинары)
Урок 6. ООП Дизайн и Solid
Доработать приложения, которые были продемонстрированы на уроке в рамках понимания работы принципов SOLID:

1)
```java
import java.io.FileWriter;
import java.io.IOException;
import java.util.Scanner;

public class Order {

    private String clientName;
    private String product;
    private int qnt;
    private int price;

    public Order(String clientName, String product, int qnt, int price) {
        this.clientName = clientName;
        this.product = product;
        this.qnt = qnt;
        this.price = price;
    }

    public String getClientName() {
        return clientName;
    }

    public String getProduct() {
        return product;
    }

    public int getQnt() {
        return qnt;
    }

    public double getPrice() {
        return price;
    }

    public void saveToJson() {
        String fileName = "order.json";
        try (FileWriter writer = new FileWriter(fileName, false)) {
            writer.write("{\n");
            writer.write("\"clientName\":\""+ clientName + "\",\n");
            writer.write("\"product\":\""+product+"\",\n");
            writer.write("\"qnt\":"+qnt+",\n");
            writer.write("\"price\":"+price+"\n");
            writer.write("}\n");
            writer.flush();
        } catch (IOException ex) {
            System.out.println(ex.getMessage());
        }
    }

    public void inputFromConsole(){
        clientName = prompt("Client name: ");
        product = prompt("Product: ");
        qnt = Integer.parseInt(prompt("Quantity: "));
        price = Integer.parseInt(prompt("Price: "));
    }

    private String prompt(String message) {
        Scanner in = new Scanner(System.in);
        System.out.print(message);
        return in.nextLine();
    }

}
```

Переработать приложение с учетом принципа SPR

```java
    public static void main(String[] args) {
        System.out.println("Введите заказ:");
        Order order = new Order("", "", 0, 0);
        order.inputFromConsole();
        order.saveToJson();
    }
```
2)*

Переработать приложение с учетом принципа DIP
```java
import java.util.ArrayList;
import java.util.List;

public class Report {

    private List<ReportItem> items; // Отчетные данные

    // расчет отчетных данных
    public void calculate(){
        items =  new ArrayList<ReportItem>();
        items.add(new ReportItem("First", (float)5));
        items.add(new ReportItem("Second", (float)6));
    }

    public void output(){
        PrintReport printReport = new PrintReport();
        printReport.output(items);
    }

}
public class PrintReport {

    public void output(List<ReportItem> items) {
        System.out.println("Output to printer");
        for (ReportItem item : items) {
            System.out.format("printer %s - %f \n\r", item.getDescription(), item.getAmount());
        }
    }

}
public class ReportItem {

    private String description;
    private float amount;

    public ReportItem(String description, float amount) {
        this.description = description;
        this.amount = amount;
    }

    public float getAmount() {
        return amount;
    }

    public String getDescription() {
        return description;
    }
}
public static void main(String[] args) {
        Report report = new Report();
        report.calculate();
        report.output();
}
```
