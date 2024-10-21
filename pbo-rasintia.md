import java.util.InputMismatchException;
import java.util.Scanner;

public class ZakatMaalCalculator {

    // Nisab default
    static double nisabEmas = 85;
    static double nisabPerak = 595;
    static double nisabTabungan = 85;
    static double nisabPerdagangan = 85;
    static double nisabPertanianIrigasi = 653;
    static double nisabPertanianAlami = 520;

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        boolean lanjut = true;

        // Menampilkan pesan selamat datang
        tampilkanHeader("Selamat Datang di Kalkulator Zakat Maal 🌙");

        while (lanjut) {
            tampilkanMenu();
            int pilihan = inputAngka(scanner, "Masukkan pilihan Anda (1-9): ");

            switch (pilihan) {
                case 1 -> ubahNisab(scanner);
                case 2 -> hitungZakatEmas(scanner);
                case 3 -> hitungZakatTabungan(scanner);
                case 4 -> hitungZakatPerniagaan(scanner);
                case 5 -> hitungZakatPertanian(scanner);
                case 6 -> hitungZakatPeternakan(scanner);
                case 7 -> hitungZakatTambang(scanner);
                case 8 -> hitungZakatInvestasi(scanner);
                case 9 -> {
                    tampilkanHeader("Terima kasih telah menggunakan kalkulator zakat. Sampai jumpa! 🌸");
                    lanjut = false;
                }
                default -> System.out.println("❌ Pilihan tidak valid. Silakan coba lagi.");
            }
        }
        scanner.close();
    }

    // Menampilkan header dengan dekorasi
    static void tampilkanHeader(String pesan) {
        System.out.println("\n==============================");
        System.out.println(" " + pesan);
        System.out.println("==============================\n");
    }

    // Menampilkan menu utama
    static void tampilkanMenu() {
        System.out.println("""
                === Pilih Jenis Zakat ===
                1. Ubah Nisab
                2. Zakat Emas, Perak, dan Logam Mulia
                3. Zakat Uang dan Tabungan
                4. Zakat Perniagaan
                5. Zakat Pertanian
                6. Zakat Peternakan
                7. Zakat Hasil Tambang
                8. Zakat Investasi dan Saham
                9. Keluar
                """);
    }

    // Metode untuk menangani input angka dengan validasi
    static int inputAngka(Scanner scanner, String pesan) {
        while (true) {
            try {
                System.out.print(pesan);
                return scanner.nextInt();
            } catch (InputMismatchException e) {
                System.out.println("❌ Input tidak valid! Masukkan angka.");
                scanner.next(); // Membersihkan input
            }
        }
    }

    // Metode untuk mengubah nisab
    static void ubahNisab(Scanner scanner) {
        tampilkanHeader("Ubah Nisab");
        System.out.print("Masukkan nisab emas (gram): ");
        nisabEmas = scanner.nextDouble();
        System.out.print("Masukkan nisab perak (gram): ");
        nisabPerak = scanner.nextDouble();
        System.out.print("Masukkan nisab tabungan (setara emas): ");
        nisabTabungan = scanner.nextDouble();
        System.out.print("Masukkan nisab perdagangan (setara emas): ");
        nisabPerdagangan = scanner.nextDouble();
        System.out.print("Masukkan nisab pertanian irigasi (kg): ");
        nisabPertanianIrigasi = scanner.nextDouble();
        System.out.print("Masukkan nisab pertanian alami (kg): ");
        nisabPertanianAlami = scanner.nextDouble();
        System.out.println("✅ Nisab berhasil diubah!\n");
    }

    // Perhitungan zakat emas
    static void hitungZakatEmas(Scanner scanner) {
        tampilkanHeader("Zakat Emas, Perak, dan Logam Mulia");
        System.out.print("Masukkan jumlah emas/perak (gram): ");
        double emas = scanner.nextDouble();
        if (emas >= nisabEmas) {
            double zakat = emas * 0.025;
            System.out.printf("Zakat: %.2f gram.%n", zakat);
        } else {
            System.out.println("❌ Jumlah emas tidak mencapai nisab.");
        }
    }

    // Perhitungan zakat tabungan
    static void hitungZakatTabungan(Scanner scanner) {
        tampilkanHeader("Zakat Uang dan Tabungan");
        System.out.print("Masukkan jumlah tabungan: ");
        double tabungan = scanner.nextDouble();
        if (tabungan >= nisabTabungan) {
            double zakat = tabungan * 0.025;
            System.out.printf("Zakat: %.2f uang.%n", zakat);
        } else {
            System.out.println("❌ Tabungan tidak mencapai nisab.");
        }
    }

    // Perhitungan zakat perniagaan
    static void hitungZakatPerniagaan(Scanner scanner) {
        tampilkanHeader("Zakat Perniagaan");
        System.out.print("Masukkan nilai dagangan: ");
        double perdagangan = scanner.nextDouble();
        if (perdagangan >= nisabPerdagangan) {
            double zakat = perdagangan * 0.025;
            System.out.printf("Zakat: %.2f uang.%n", zakat);
        } else {
            System.out.println("❌ Dagangan tidak mencapai nisab.");
        }
    }

    // Perhitungan zakat pertanian
    static void hitungZakatPertanian(Scanner scanner) {
        tampilkanHeader("Zakat Pertanian");
        System.out.println("Pilih metode pengairan:");
        System.out.println("  1. Irigasi (dengan biaya)");
        System.out.println("  2. Pengairan alami (air hujan)");
        int metode = inputAngka(scanner, "Masukkan pilihan: ");
        System.out.print("Masukkan jumlah hasil panen (kg): ");
        double hasil = scanner.nextDouble();

        if (metode == 1 && hasil >= nisabPertanianIrigasi) {
            double zakat = hasil * 0.05;
            System.out.printf("Zakat: %.2f kg.%n", zakat);
        } else if (metode == 2 && hasil >= nisabPertanianAlami) {
            double zakat = hasil * 0.10;
            System.out.printf("Zakat: %.2f kg.%n", zakat);
        } else {
            System.out.println("❌ Hasil panen tidak mencapai nisab.");
        }
    }

    // Perhitungan zakat peternakan
    static void hitungZakatPeternakan(Scanner scanner) {
        tampilkanHeader("Zakat Peternakan");
        System.out.print("Masukkan jumlah ternak: ");
        int ternak = scanner.nextInt();
        if (ternak >= 40) {
            int zakat = ternak / 40;
            System.out.printf("Zakat: %d ekor.%n", zakat);
        } else {
            System.out.println("❌ Jumlah ternak tidak mencapai nisab.");
        }
    }

    // Perhitungan zakat tambang
    static void hitungZakatTambang(Scanner scanner) {
        tampilkanHeader("Zakat Hasil Tambang");
        System.out.print("Masukkan nilai hasil tambang: ");
        double tambang = scanner.nextDouble();
        double zakat = tambang * 0.025;
        System.out.printf("Zakat: %.2f uang.%n", zakat);
    }

    // Perhitungan zakat investasi
    static void hitungZakatInvestasi(Scanner scanner) {
        tampilkanHeader("Zakat Investasi dan Saham");
        System.out.print("Masukkan nilai investasi/saham: ");
        double investasi = scanner.nextDouble();
        if (investasi >= nisabPerdagangan) {
            double zakat = investasi * 0.025;
            System.out.printf("Zakat: %.2f uang.%n", zakat);
        } else {
            System.out.println("❌ Investasi tidak mencapai nisab.");
        }
    }
}
