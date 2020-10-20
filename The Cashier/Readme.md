# The Cashier Apps
Merupakan aplikasi kasir sederhana untuk melakukan perhitungan transaksi barang/jasa dengan menginputkan jumlah dan harganya.
## Scope & Functionalities
- user dapat memasukkan nama 
- user dapat memasukkan jumlah dan harga
- user dapat memilih barang / jasa
- dapat melihat tampilan total dari yang diimputkan

## How Does it works?
Diawali dari method `MainWidow` pada class `MainWindow.xaml.cs` kita mendeklarasikan...
```
 private Calculator calculator;
        public MainWindow()
        {
            InitializeComponent();
            calculator = new Calculator();
            listBox.ItemsSource = calculator.GetListItem();
        }
```
Pemilihan barang/jasa terdapat pada class ```Item.cs``` =
```
public string GetTitle()
        {
            return title;
        }
        public int GetQuantity()
        {
            return quantity;
        }
        public string getType()
        {
            return type;
        }
        public double GetPrice()
        {
            return price;
        }
        public double GetSubTotal()
        {
            subtotal = price * quantity;
            return subtotal;
        }
```
Perhitungan semua barang/jasa yang dipilih terdapat pada class ```Calculator.cs``` =
```
  public void AddItem(Item item)
        {
            this.listItem.Add(item);
            this.total += item.GetSubTotal();
        }

```
Menampilkan apa saja yang ada dengan menekan button pada listBox pada class ```MainWindow.xaml.cs``` dengan cara ....
```
private void AddButton_Click(object sender, RoutedEventArgs e)
{
    string title = itemNameBox.Text;
    int quantity = int.Parse(quantityBox.Text);
    string type = typeBox.Text;
    double price = double.Parse(priceBox.Text);

    Item item = new Item(new Random().Next(), title, quantity, price, price, type);
    calculator.AddItem(item);
    double total = calculator.GetTotal();

    totalLabel.Content = String.Format("Rp {0}", total);
    listBox1.Items.Refresh();
}

```
