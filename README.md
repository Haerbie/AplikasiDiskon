# Tugas 3: Aplikasi Perhitungan Diskon

### Pembuat
- **Nama**: Muhammad Irwan Habibie
- **NPM**: 2210010461

---

## 1. Deskripsi Program
Aplikasi ini memungkinkan pengguna untuk:
- Memasukkan harga asli barang.
- Memilih persentase diskon yang ingin diterapkan.
- Menghitung harga akhir setelah diskon serta jumlah penghematan yang diperoleh.

## 2. Komponen GUI
- **JFrame**: Window utama aplikasi.
- **JPanel**: Panel untuk menampung komponen.
- **JLabel**: Label untuk menunjukkan harga asli, persentase diskon, dan hasil.
- **JTextField**: Input untuk memasukkan harga asli barang.
- **JComboBox**: Dropdown untuk memilih persentase diskon.
- **JButton**: Tombol untuk melakukan perhitungan diskon.

## 3. Logika Program
- Melakukan perhitungan aritmatika untuk menentukan harga akhir dan penghematan berdasarkan persentase diskon yang dipilih.
- Penanganan eksepsi untuk validasi input, memastikan pengguna memasukkan angka untuk harga asli.

## 4. Events
Menggunakan **ActionListener** dan **ItemListener** untuk menangani interaksi pengguna:

### A. Tombol Hitung
Menghitung harga akhir setelah diskon diterapkan dan menampilkan hasil.
```java
    private void jButton1ActionPerformed(java.awt.event.ActionEvent evt) {                                         
        try {
            // Cek apakah hargaAsliTextField kosong atau tidak valid
            if (hargaAsliTextField.getText().isEmpty() || hargaAsliTextField.getText().equals("Rp ")) {
                JOptionPane.showMessageDialog(this, "Silakan masukkan harga asli.", "Error", JOptionPane.ERROR_MESSAGE);
                return;
            }

            // Ambil harga asli dari JTextField dan hilangkan "Rp " di depannya
            double hargaAsli = Double.parseDouble(hargaAsliTextField.getText().replace("Rp ", ""));

            // Tentukan diskon persentase dari JSlider atau JComboBox
            int diskonPersen;
            if (diskonSlider.getValue() > 0) {
                diskonPersen = diskonSlider.getValue();
            } else {
                String diskonStr = (String) persentaseDiskonComboBox.getSelectedItem();
                diskonPersen = Integer.parseInt(diskonStr.replace("%", ""));
            }

            // Ambil kode kupon dari JTextField
            String kodeKupon = kodeKuponTextField.getText().trim();

            // Tambahan diskon jika kode kupon valid
            if (kodeKupon.equalsIgnoreCase("DISKON10")) {
                diskonPersen += 10;
            } else if (!kodeKupon.isEmpty()) {
                JOptionPane.showMessageDialog(this, "Kode kupon tidak valid.", "Info", JOptionPane.INFORMATION_MESSAGE);
            }

            // Hitung penghematan dan harga akhir
            double penghematan = hargaAsli * diskonPersen / 100;
            double hargaAkhir = hargaAsli - penghematan;

            // Tampilkan hasil pada JTextField dengan prefix "Rp "
            penghematanTextField.setText("Rp " + String.format("%.2f", penghematan));
            hargaAkhirTextField.setText("Rp " + String.format("%.2f", hargaAkhir));

            // Tambahkan hasil ke riwayat
            String hasilRiwayat = "Harga Asli: Rp " + hargaAsli +
                                  ", Diskon: " + diskonPersen + "%" +
                                  ", Penghematan: Rp " + String.format("%.2f", penghematan) +
                                  ", Harga Akhir: Rp " + String.format("%.2f", hargaAkhir) + "\n";
            riwayatTextArea.append(hasilRiwayat);
        } catch (NumberFormatException e) {
            JOptionPane.showMessageDialog(this, "Masukkan nilai yang valid.", "Error", JOptionPane.ERROR_MESSAGE);
        }
    }  
```
### B. ItemListener pada JComboBox
Memilih persentase diskon yang akan diterapkan pada harga asli.
```java
    public DiskonFrame() {
        initComponents();
        persentaseDiskonComboBox.addItem("10%");
        persentaseDiskonComboBox.addItem("20%");
        persentaseDiskonComboBox.addItem("30%");
    }
```

## 5. Variasi
Aplikasi ini memiliki variasi tambahan berikut:

### A. Kode Kupon Diskon Tambahan
Menambahkan opsi untuk memasukkan kode kupon diskon tambahan agar pengguna bisa mendapatkan diskon ekstra.
```java
            // Ambil kode kupon dari JTextField
            String kodeKupon = kodeKuponTextField.getText().trim();

            // Tambahan diskon jika kode kupon valid
            if (kodeKupon.equalsIgnoreCase("DISKON10")) {
                diskonPersen += 10;
            } else if (!kodeKupon.isEmpty()) {
                JOptionPane.showMessageDialog(this, "Kode kupon tidak valid.", "Info", JOptionPane.INFORMATION_MESSAGE);
            }
```
### B. JSlider
Menggunakan **JSlider** sebagai alternatif untuk memilih persentase diskon.
```java
    private void diskonSliderStateChanged(javax.swing.event.ChangeEvent evt) {                                          
        // Update label persentase sesuai dengan nilai slider
        int sliderValue = diskonSlider.getValue();
        jLabel7.setText("Persentase Diskon: " + sliderValue + "%");
    }  
```

### C. Riwayat Perhitungan Diskon
Menyediakan riwayat perhitungan diskon yang telah dilakukan untuk membantu pengguna melihat diskon yang sudah diterapkan sebelumnya.
```java
            // Tambahkan hasil ke riwayat
            String hasilRiwayat = "Harga Asli: Rp " + hargaAsli +
                                  ", Diskon: " + diskonPersen + "%" +
                                  ", Penghematan: Rp " + String.format("%.2f", penghematan) +
                                  ", Harga Akhir: Rp " + String.format("%.2f", hargaAkhir) + "\n";
            riwayatTextArea.append(hasilRiwayat);
```
## 6. Tampilan Aplikasi Saat di Run

![TampilanDiskon](https://github.com/user-attachments/assets/2e924e34-938b-4c8a-8389-59a74edac539)

## 7. Indikator Penilaian

| No  | Komponen          | Persentase |
| :-: | ------------------ | :--------: |
|  1  | Komponen GUI      |     20%    |
|  2  | Logika Program    |     20%    |
|  3  | Events            |     15%    |
|  4  | Kesesuaian UI     |     15%    |
|  5  | Memenuhi Variasi  |     30%    |
|     | **TOTAL**         |  **100%**  |

--- 
