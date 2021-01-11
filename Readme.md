# Menu dan Promo
Aplikasi simulasi pembelian makanan/minuman sederhana menggunakan promo/voucher.

## Fungsi
- User dapat melihat daftar makanan, minuman, dan voucher atau promo
- User dapat memasukkan atau menghapus makanan, minuman, dan voucher atau promo
- User dapat hanay bisa menggunakan satu voucher
- User dapat melihat total harga beserta potongannya

## How Does it works?
Simulasi ini menggunakan 4 buah model dan 3 buah controller yang bertujuan untuk menjalankan program tersebut

Fungsi beberapa kode:

`Penawaran.xaml.cs` untuk menampilkan daftar makanan dan minuman dalam listbox
```csharp
        private void generateContentPenawaran()
        {
            Item coffeLate = new Item("Coffe Late", 30000);
            Item blackTea = new Item("BlackTea", 20000);
            Item milkShake = new Item("Milk Shake", 15000);
            Item watermelonJuice = new Item("Watermelon Juice", 25000);
            Item lemonSquash = new Item("Lemon Squash", 30000);
            Item pizza = new Item("Pizza", 75000);
            Item friedRice = new Item("Fried Rice Special", 45000);

            Penawarancontroller.addItem(coffeLate);
            Penawarancontroller.addItem(blackTea);
            Penawarancontroller.addItem(milkShake);
            Penawarancontroller.addItem(watermelonJuice);
            Penawarancontroller.addItem(lemonSquash);
            Penawarancontroller.addItem(pizza);
            Penawarancontroller.addItem(friedRice);

            listPenawaran.Items.Refresh();
        }
```

<br>

`PilihVoucher.xaml.cs` untuk menampilkan daftar voucher dalam listbox
```csharp
        private void generateListVoucher()
        {
            Model.Voucher awalTahun = new Model.Voucher(title: "Promo Awal Tahun Diskon 25%", discInPercent: 25);
            Model.Voucher tebusMurah = new Model.Voucher(title: "Promo Tebus Murah Diskon 30% atau max. 30.000", discInPercent: 30);
            Model.Voucher promoNatal = new Model.Voucher(title: "Promo Natal Potongan 10000", disc: 10000);

            voucherController.addItem(awalTahun);
            voucherController.addItem(tebusMurah);
            voucherController.addItem(promoNatal);

            DaftarVoucher.Items.Refresh();
        }
```

<br>

`MainWindow.xaml.cs` digunakan untuk inisialisasi dan membuat beberapa instance untuk digunakan dalam list `KeranjangBelanja`
```csharp
        public MainWindow()
        {
            InitializeComponent();

            payment = new Payment(this);

            KeranjangBelanja keranjangBelanja = new KeranjangBelanja(payment, this);

            controller = new MainWindowController(keranjangBelanja);

            listBoxPesanan.ItemsSource = controller.getSelectedItems();
            listBoxPakaiVoucher.ItemsSource = controller.getSelectedVouchers();

            initializeView();

```