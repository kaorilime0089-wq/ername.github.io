namespace Shop.Models;

public class Order
{
    public int Id { get; set; }

    public string OrderNumber { get; set; }
        = "";

    public string ProductId { get; set; }
        = "";

    public string ProductName { get; set; }
        = "";

    public string CustomerName { get; set; }
        = "";

    public string CustomerEmail { get; set; }
        = "";

    public int Quantity { get; set; }

    public int Amount { get; set; }

    public string PaymentMethod { get; set; }
        = "bank";

    public string Status { get; set; }
        = "WaitingForPayment";

    public DateTime CreatedAt { get; set; }

    public DateTime? PaidAt { get; set; }

    public bool ProductDelivered { get; set; }
}

