import java.text.NumberFormat;
import java.util.Locale;
import java.util.Scanner;

class Pegawai {
    private String nama;
    private String jabatan;
    private double gajiPokok;
    private double tunjangan;
    private double potongan;
    private double bonus;

    public Pegawai() {
        this.nama = "";
        this.jabatan = "";
        this.gajiPokok = 0.0;
        this.tunjangan = 0.0;
        this.potongan = 0.0;
        this.bonus = 0.0;
    }

    public Pegawai(String nama, String jabatan, double gajiPokok, double tunjangan, double potongan, double bonus) {
        this.nama = nama;
        this.jabatan = jabatan;
        this.gajiPokok = gajiPokok;
        this.tunjangan = tunjangan;
        this.potongan = potongan;
        this.bonus = bonus;
    }

    public String getNama() {
        return nama;
    }

    public void setNama(String nama) {
        this.nama = nama;
    }

    public void setJabatan(String jabatan) {
        this.jabatan = jabatan;
    }

    public void setGajiPokok(double gajiPokok) {
        this.gajiPokok = gajiPokok;
    }

    public void setTunjangan(double tunjangan) {
        this.tunjangan = tunjangan;
    }

    public void setPotongan(double potongan) {
        this.potongan = potongan;
    }

    public void setBonus(double bonus) {
        this.bonus = bonus;
    }

    public double hitungGajiTotal() {
        return gajiPokok + tunjangan + bonus - potongan;
    }

    public void displayInfo() {
        System.out.println("\n====================================");
        System.out.println("Nama Pegawai   : " + nama);
        System.out.println("Jabatan        : " + jabatan);
        System.out.println("Gaji Pokok     : " + formatRupiah(gajiPokok));
        System.out.println("Tunjangan      : " + formatRupiah(tunjangan));
        System.out.println("Bonus          : " + formatRupiah(bonus));
        System.out.println("Potongan       : " + formatRupiah(potongan));
        System.out.println("Total Gaji     : " + formatRupiah(hitungGajiTotal()));
        System.out.println("====================================\n");
    }

    public void tambahBonus(double tambahanBonus) {
        this.bonus += tambahanBonus;
    }

    private String formatRupiah(double angka) {
        NumberFormat formatRupiah = NumberFormat.getNumberInstance(new Locale("id", "ID"));
        return formatRupiah.format(angka);
    }
}

public class Pemjutsulit{
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);

        Pegawai pegawai1 = new Pegawai();
        System.out.print("Masukkan Nama Pegawai: ");
        pegawai1.setNama(input.nextLine());
        System.out.print("Masukkan Jabatan: ");
        pegawai1.setJabatan(input.nextLine());

        pegawai1.setGajiPokok(masukkanAngka("Masukkan Gaji Pokok: ", input));
        pegawai1.setTunjangan(masukkanAngka("Masukkan Tunjangan: ", input));
        pegawai1.setPotongan(masukkanAngka("Masukkan Potongan: ", input));
        pegawai1.setBonus(masukkanAngka("Masukkan Bonus: ", input));

        pegawai1.displayInfo();

        input.nextLine();
        System.out.print("Masukkan Nama Pegawai Kedua: ");
        String nama2 = input.nextLine();
        System.out.print("Masukkan Jabatan: ");
        String jabatan2 = input.nextLine();

        double gajiPokok2 = masukkanAngka("Masukkan Gaji Pokok: ", input);
        double tunjangan2 = masukkanAngka("Masukkan Tunjangan: ", input);
        double potongan2 = masukkanAngka("Masukkan Potongan: ", input);
        double bonus2 = masukkanAngka("Masukkan Bonus: ", input);

        Pegawai pegawai2 = new Pegawai(nama2, jabatan2, gajiPokok2, tunjangan2, potongan2, bonus2);

        pegawai2.displayInfo();

        double tambahanBonus = masukkanAngka("Masukkan tambahan bonus untuk " + pegawai1.getNama() + ": ", input);
        pegawai1.tambahBonus(tambahanBonus);

        System.out.println("Setelah Bonus Ditambahkan:");
        pegawai1.displayInfo();

        input.close();
    }

    public static double masukkanAngka(String pesan, Scanner input) {
        double angka = 0;
        while (true) {
            System.out.print(pesan);
            if (input.hasNextDouble()) {
                angka = input.nextDouble();
                break;
            } else {
                System.out.println("Input harus berupa angka! Silakan coba lagi.");
                input.next();
            }
        }
        return angka;
    }
}
