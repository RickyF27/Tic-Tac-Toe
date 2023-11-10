# Tic-Tac-Toe

Tuliskan semua Java Code diatas, kemudian pelajari code nya, dan ubahkan beberapa bagian untuk melihat perubahannya.

Jawaban :

Permainan tic tac toe dapat menggunakan algoritma heuristic untuk menyelesaikan masalah dan mendapatlan solusi yang optimal. Tic tac toe ini memiliki initial state berupa puzzle dengan ukuran 8 yang tidak berisikan apa-apa. Ketika pemain pertama memilih salah satu ubin, maka ubin tersebut akan diberikan tanda untuk menandakan bahwa ubin tersebut milik pemain pertama. Pemain kedua harus menghalangi pemain pertama untuk membuat tanda yang berjajaran seperti vertikal, horizontal, atau diagonal. Permainan ini akan mencapai goal state ketika salah satu pemain sudah berhasil mendaratkan tanda di 3 ubin secara vertikal, horizontal, maupun diagonal.

Solusi dari permasalahan ini dapat dicapai dengan membuat topologi Tree, kemudian setiap langkah dari pemain pertama atau kedua akan menjadikan initial state selanjutnya, kemudian langkah tersebut akan dijadikan sebagai initial state yang baru sampai menemukan goal statenya. Seperti gambar dibawah ini.

![image](https://github.com/RickyF27/Tic-Tac-Toe/assets/149030301/e4caf3b6-d6f0-421a-bbfb-4021fd6e78ed)

Code dari penyelesaian permainan Tic Tac Toe ini bisa dilihat dibawah ini melalui bahasa pemrograman python, hal itu dikarenakan bahasa pemrograman python ini sangat mudah untuk dipahami dikarenakan sifatnya yang sederhana.

    import tkinter as tk
    from tkinter import messagebox

Code diatas, kita diharuskan untuk mengimpor modul tkinter sehingga dapat memasukkan komponen antarmuka pengguna grafis (GUI) ke dalam program. Selain mengimpor modul tinker, kita juga diharuskan untuk mengimpor modul messagebox yang digunakan untuk menampilkan kotak pesan kepada pengguna dalam GUI seperti pesan informasi, peringatan, atau konfirmasi.

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

Fungsi diatas digunakan untuk mengecekan apakah ada pemenang atau hasil seri dalam permainan Tic-Tac-Toe. Jika ada pemain yang berhasil mencapai kondisi kemenangan, maka fungsi ini akan mengembalikan simbol pemenang apakah "X" atau "O". Namun, jika tidak ada pemenang yang terdeteksi, maka hasil yang dikembalikan akan berupa None saja. Hal itu bisa dilakukan karena fungsi ini mengecek setiap kolom vertikal, horizontal maupun diagonal dengan simbol "X" atau "O".

    # Fungsi untuk menangani klik pada papan permainan
    winner = None
    turn = True

Variabel winner diatas digunakan sebagai tempat yang mengimpan informasi mengenai pemenang didalam permainan, sedangkan variabel turn digunakan untuk menentukan giliran pemain yang sedang beraksi, ketika nilai turn = true maka giliran pemain "X" yang beraksi sedangkan jika nilai turn = false maka giliran pemain "O" yang beraksi.

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


Fungsi diatas digunakan untukk mengelola apabila kotak yang diklik belum terisi dan belum ada pemenang, maka kotak tersebut akan diisi dengan "X" atau "O" sesuai dengan giliran pemain yang beraksi. Sedangkan fungsi check_winner() digunakan untuk memeriksa apakah ada pemenang dalam permainan, dimana ketika ada pemenang, pesan kemenangan akan ditampilkan di dalam kotak pesan, dan semua tombol akan dinonaktifkan.

    # Fungsi untuk me-reset permainan
    def reset_game():
    global board, turn, winner
    board = [["" for _ in range(3)] for _ in range(3)]
    turn = True
    winner = None
    for row in buttons:
        for button in row:
            button.config(text="", state="normal")

Fungsi diatas digunakan untuk mengembalikan permainan ke keadaan awal.

    # Membuat jendela utama
    root = tk.Tk()
    root.title("Tic-Tac-Toe")

Kode diatas digunakan untuk membuat jendela utama dengan judul "Tic-Tac-Toe".

    # Membuat papan permainan
    board = [["" for _ in range(3)] for _ in range(3)]
    buttons = [[None for _ in range(3)] for _ in range(3)]
    for i in range(3):
        for j in range(3):
            buttons[i][j] = tk.Button(root, text="", font=("normal", 20), width=5, height=2,
                                 command=lambda i=i, j=j: on_click(i, j))
            buttons[i][j].grid(row=i, column=j)

Kode diatas digunakanb untuk menghasilkan sebuah papan permainan 3x3 yang terdiri dari tombol-tombol yang dapat diaktifkan dengan mengklikny, fungsi on_click() digunakan untuk menangani tindakan klik.

    # Membuat tombol reset
    reset_button = tk.Button(root, text="Reset Game", font=("normal", 16), command=reset_game)
    reset_button.grid(row=3, columnspan=3)

Kode diatas digunakan untukk menciptakan sebuah tombol dengan label "Reset Game," yang akan mengaktifkan fungsi reset_game() ketika tombol tersebut ditekan.

    # Menjalankan GUI
    root.mainloop()

Kode diatas memungkinkan GUI untuk selalu aktif dan siap menerima masukan dari pengguna sampai ada interaksi baru untuk mengeksekusi program.
