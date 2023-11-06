# Permainan TIC TAC TOE
# Tugas
Tuliskan semua Java Code diatas, kemudian pelajari code nya, dan ubahkan beberapa bagian untuk melihat perubahannya.
# Dasar Teori
Penyelesaian masalah permainan tic tac toe dapat menggunakan algoritma heuristic untuk mencapai solusi yang optimal. Pada modul ini memperlihatkan bagaimana membuat sebuah permainan tic tac toe. Initial state dari permainan ini adalah puzzle ukuran 8 yang tidak berisikan apa-apa. Ketika pemain pertama menekan salah satu ubin, maka ubin tersebut akan diberikan tanda silang. Pemain kedua harus menghalangi pemain pertama untuk membuat tanda silang berjajaran baik secara vertikal, horizontal, atau diagonal. Permainan ini akan berakhir (goal state) ketika salah seorang pemain sudah menderetkan tanda meraka masing-masing baik secara vertikal, horizontal, atau diagonal.

Solusi dari permasalahan ini dapat dilakukan dengan membuat topologi Tree, kemudian setiap langkah dari pemain pertama atau kedua akan menjadikan initial state selanjutnya, kemudian langkah tersebut akan dijadikan sebagai initial state yang baru sampai menemukan goal statenya.Ilustrasi penyelesaian masalah permainan tic tac toe ini dapat dilihat melalui Gambar.

![image](https://github.com/kausaraghnia/kausaraghnia/assets/148691014/da9b2e86-fcd6-4ea2-bd07-02ade07eb673)

# Code dan Pejelasan
Pada kali ini, saya memanfaatkan bahasa pemrograman Python. Python adalah pilihan yang sangat baik untuk pemula dalam dunia pemrograman, karena sifatnya yang mudah dan sederhana. Python memiliki berbagai fitur yang membuatnya populer seperti sintaksis yang bersahabat, dukungan komunitas yang besar, dan berbagai pustaka yang siap digunakan menjadikannya pilihan yang sangat menguntungkan untuk proyek-proyek pemrograman.

    import tkinter as tk
    from tkinter import messagebox

Dalam kode ini, kita mengimpor modul tkinter untuk memasukkan komponen antarmuka pengguna grafis (GUI) ke dalam program, sehingga kita dapat membangun aplikasi dengan elemen-elemen seperti jendela, tombol, teks, dan lainnya. Selain itu, kita juga mengimpor modul messagebox yang memungkinkan kita untuk menampilkan kotak pesan kepada pengguna dalam GUI seperti pesan informasi, peringatan, atau konfirmasi. Kombinasi dari modul-modul ini memungkinkan kita untuk membuat aplikasi dengan antarmuka yang interaktif dan dapat memberikan umpan balik kepada pengguna.

    # Fungsi untuk mengecek apakah ada pemenang atau seri
    def check_winner():
    for i in range(3):
        if board[i][0] == board[i][1] == board[i][2] != "":
            return board[i][0]
        if board[0][i] == board[1][i] == board[2][i] != "":
            return board[0][i]
    if board[0][0] == board[1][1] == board[2][2] != "":
        return board[0][0]
    if board[0][2] == board[1][1] == board[2][0] != "":
        return board[0][2]
    if all(board[i][j] != "" for i in range(3) for j in range(3)):
        return "Draw"
    
    return None

Fungsi ini berperan untuk melakukan pengecekan apakah ada pemenang atau hasil seri dalam permainan Tic-Tac-Toe. Untuk mencapai tujuan ini, ia melakukan pengecekan pada setiap baris, kolom, dan diagonal dalam papan permainan guna menentukan apakah ada pemain yang berhasil membentuk garis horizontal, vertikal, atau diagonal dengan simbol "X" atau "O". Jika ada pemain yang berhasil mencapai kondisi kemenangan, fungsi ini akan mengembalikan simbol pemenang apakah "X" atau "O" yang menjadi pememang. Namun, jika tidak ada pemenang yang terdeteksi maka hasil yang dikembalikan akan berupa None yang berarti menandakan bahwa permainan berakhir dengan hasil seri.

    # Fungsi untuk menangani klik pada papan permainan
    winner = None
    turn = True

Variabel winner berperan sebagai wadah yang digunakan untuk menyimpan informasi mengenai pemenang dari permainan yang sedang berlangsung. Sementara itu, variabel turn memiliki peran penting dalam menentukan giliran pemain yang sedang beraksi dalam permainan tersebut. Ketika nilai turn adalah True, berarti giliran saat ini adalah milik pemain "X," sedangkan ketika nilai turn adalah False, giliran pemain saat ini adalah "O." Dengan demikian, kedua variabel ini memainkan peran kunci dalam mengatur dan melacak perkembangan permainan.

    def on_click(row, col):
    global turn, winner

    if board[row][col] == "" and not winner:
        if turn:
            board[row][col] = "X"
            buttons[row][col].config(text="X", state="disabled")
        else:
            board[row][col] = "O"
            buttons[row][col].config(text="O", state="disabled")

        turn = not turn

        result = check_winner()
        if result:
            winner = result
            messagebox.showinfo("Tic-Tac-Toe", f"Player {winner} wins!")
            for row in buttons:
                for button in row:
                    button.config(state="disabled")


Fungsi ini mengelola tindakan ketika pemain mengklik kotak di papan permainan. Apabila kotak yang diklik belum terisi dan belum ada pemenang dalam permainan, maka kotak tersebut akan diisi dengan "X" atau "O" sesuai dengan giliran pemain, dan tombol akan dinonaktifkan. Selanjutnya, fungsi check_winner() akan dipanggil untuk memeriksa apakah ada pemenang dalam permainan. Jika ada pemenang, pesan kemenangan akan ditampilkan di dalam kotak pesan, dan semua tombol akan dinonaktifkan.

    # Fungsi untuk me-reset permainan
    def reset_game():
    global board, turn, winner
    board = [["" for _ in range(3)] for _ in range(3)]
    turn = True
    winner = None
    for row in buttons:
        for button in row:
            button.config(text="", state="normal")

Fungsi ini bertujuan untuk mengembalikan permainan ke keadaan awal. Semua variabel global diatur ulang, papan permainan dikosongkan, dan tombol-tombol dikembalikan ke kondisi awal sehingga pemain dapat memulai permainan dari awal tanpa kebingungan.

    # Membuat jendela utama
    root = tk.Tk()
    root.title("Tic-Tac-Toe")

Kode ini untuk membuat jendela utama dengan judul "Tic-Tac-Toe".

    # Membuat papan permainan
    board = [["" for _ in range(3)] for _ in range(3)]
    buttons = [[None for _ in range(3)] for _ in range(3)]
    for i in range(3):
        for j in range(3):
            buttons[i][j] = tk.Button(root, text="", font=("normal", 20), width=5, height=2,
                                 command=lambda i=i, j=j: on_click(i, j))
            buttons[i][j].grid(row=i, column=j)

Kode ini menghasilkan sebuah papan permainan 3x3 yang terdiri dari tombol-tombol yang dapat diaktifkan dengan mengkliknya. Setiap tombol awalnya tidak memiliki teks, dan mereka diberikan pengaturan menggunakan fungsi on_click() untuk menangani tindakan klik.

    # Membuat tombol reset
    reset_button = tk.Button(root, text="Reset Game", font=("normal", 16), command=reset_game)
    reset_button.grid(row=3, columnspan=3)

Kode ini menciptakan sebuah tombol dengan label "Reset Game," yang akan mengaktifkan fungsi reset_game() ketika tombol tersebut ditekan. Ini memungkinkan pengguna untuk mengulang permainan atau mereset kondisi permainan ke awal saat tombol ditekan.

    # Menjalankan GUI
    root.mainloop()

Dengan kode ini, loop utama GUI tkinter dimulai, memungkinkan GUI untuk aktif dan siap menerima masukan dari pengguna. GUI akan tetap berjalan dan menunggu sampai ada interaksi atau input yang diberikan oleh pengguna sebelum melanjutkan eksekusi program.

Setelah menjalankannya, program akan menghasilkan tampilan GUI Tic-Tac-Toe seperti yang terlihat di bawah ini.

![image](https://github.com/kausaraghnia/kausaraghnia/assets/148691014/2b8fd1b9-ab19-4796-a2e9-163896608176)

Nanti dapat mengklik kolom, di mana klik pertama akan menampilkan simbol X, dan setiap klik kedua akan menampilkan simbol O, hingga terbentuk susunan X atau O yang sejajar baik secara vertikal, diagonal, maupun horizontal. Berikut adalah contoh hasil permainannya.

![image](https://github.com/kausaraghnia/kausaraghnia/assets/148691014/e1ea7718-78c3-4cd1-872f-aaaf589b2deb) ![image](https://github.com/kausaraghnia/kausaraghnia/assets/148691014/1ef667a2-ea1f-40d9-94d2-52381a3b4d32)

Klik tombol reset maka nanti tampilan akan kosong lagi seperti gambar tampilan pertama.
