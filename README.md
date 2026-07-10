## Week 01 Evidence

> Evidence from the end of the module Create a web API with ASP.NET Core controllers showing the existing content, and your additional record.

```HTTP/1.1 200 OK
Connection: close
Content-Type: application/json; charset=utf-8
Date: Fri, 10 Jul 2026 18:33:04 GMT
Server: Kestrel
Transfer-Encoding: chunked

[
  {
    "id": 1,
    "name": "Classic Italian",
    "isGlutenFree": false
  },
  {
    "id": 2,
    "name": "Veggie",
    "isGlutenFree": true
  },
  {
    "id": 3,
    "name": "Surpreme",
    "isGlutenFree": false
  }
]```

> A text copy of your working sales summary function for Part 2.

Code:
```string GenerateSalesReport(IEnumerable<string> salesFiles)
{
    StringBuilder report = new StringBuilder();

    double salesTotal = 0;

    report.AppendLine("Sales Summary");
    report.AppendLine("----------------------------");

    report.AppendLine();
    report.AppendLine("Details:");

    foreach (var file in salesFiles)
    {
        string salesJson = File.ReadAllText(file);

        SalesData? data = JsonConvert.DeserializeObject<SalesData?>(salesJson);

        double fileTotal = data?.Total ?? 0;
        salesTotal += fileTotal;

        report.AppendLine(
            $"{Path.GetFileName(file)}: {fileTotal:C}"
        );
    }

    report.Insert(
        report.ToString().IndexOf("Details:"),
        $"Total Sales: {salesTotal:C}\n\n"
    );

    return report.ToString();
}
```

Generated Result:
```Sales Summary
----------------------------

Total Sales: $2,012.20

Details:
sales.json: $88.88
sales.json: $501.22
salestotals.json: $0.00
sales.json: $1,234.22
salestotals.json: $0.00
sales.json: $99.00
salestotals.json: $0.00
sales.json: $88.88
salestotals.json: $0.00
```