from tkinter import *
from tkinter import messagebox

class Mahasiswa:
    def __init__(self, nama, nim, tugas, uts, uas):
        self.nama = nama
        self.nim = nim
        self.tugas = tugas
        self.uts = uts
        self.uas = uas

    def hitung_rata_rata(self, tipe):
        if tipe == "Tugas":
            return sum(self.tugas) / len(self.tugas)
        elif tipe == "UTS":
            return sum(self.uts) / len(self.uts)
        elif tipe == "UAS":
            return sum(self.uas) / len(self.uas)

def open_assessment_window(nama, nim, tipe, main_window):
    assessment_window = Toplevel()
    assessment_window.title(f"Hitung Rata-Rata Nilai {tipe}")
    assessment_window.config(bg="lightblue")

    # Calculate the position for the window to be centered
    window_width = 400
    window_height = 500
    screen_width = assessment_window.winfo_screenwidth()
    screen_height = assessment_window.winfo_screenheight()
    position_top = int((screen_height - window_height) / 2)
    position_right = int((screen_width - window_width) / 2)
    assessment_window.geometry(f"{window_width}x{window_height}+{position_right}+{position_top}")

    def calculate_average_grade():
        try:
            scores = [entry_score[i].get() for i in range(6)]

            # Convert to float and validate
            def convert_and_validate(entries):
                values = []
                for entry in entries:
                    if entry.strip() == "":
                        raise ValueError("Semua nilai harus diisi")
                    try:
                        value = float(entry)
                    except ValueError:
                        raise ValueError("Nilai harus berupa angka")
                    if not 0 <= value <= 100:
                        raise ValueError("Nilai harus antara 0 dan 100")
                    values.append(value)
                return values

            scores = convert_and_validate(scores)

            # Object Oriented Programming
            if tipe == "Tugas":
                mahasiswa = Mahasiswa(nama, nim, scores, [], [])
            elif tipe == "UTS":
                mahasiswa = Mahasiswa(nama, nim, [], scores, [])
            elif tipe == "UAS":
                mahasiswa = Mahasiswa(nama, nim, [], [], scores)
            average_grade = mahasiswa.hitung_rata_rata(tipe)

            # Perulangan (untuk mengubah warna latar belakang)
            colors = ["lightblue", "lightgreen", "lightyellow", "lightpink"]
            for color in colors:
                if color == assessment_window.cget("bg"):
                    continue
                assessment_window.config(bg=color)
                break

            # Add student to listbox
            students_listbox.insert(END, f"{nama} ({nim}) - Rata-rata {tipe}: {average_grade:.2f}")

            # Clear entries after adding
            for entry in entry_score:
                entry.delete(0, END)

        except ValueError as e:
            messagebox.showerror("Error", str(e))

    def back_to_main():
        assessment_window.destroy()
        main_window.deiconify()

    # Configure grid layout
    assessment_window.columnconfigure(0, weight=1)
    assessment_window.columnconfigure(1, weight=1)

    # Button to go back to the main window
    button_back = Button(assessment_window, text="Kembali", command=back_to_main, font=("Arial", 10))
    button_back.grid(row=0, column=0, sticky=W, padx=10, pady=10)

    # Welcome Label
    label_welcome = Label(assessment_window, text=f"Selamat datang, {nama}! Silahkan masukkan nilai rata-rata {tipe} Anda.", font=("Arial", 14), bg="lightblue")
    label_welcome.grid(row=1, column=0, columnspan=2, pady=10)

    # Entries for Scores
    subjects = ["Alpro", "PPB", "DKP", "Aljabar Linear", "Kimia", "Fisika Dasar", "Matematika Teknik"]
    entry_score = []
    for i in range(6):
        label = Label(assessment_window, text=f"Nilai Mata Kuliah {subjects[i]}:", font=("Arial", 12), bg="lightblue")
        label.grid(row=2+i, column=0, sticky=E, padx=10, pady=5)
        entry = Entry(assessment_window, font=("Arial", 12), width=10)
        entry.grid(row=2+i, column=1, sticky=W, padx=10, pady=5)
        entry_score.append(entry)

    # Tombol Hitung
    button_calculate = Button(assessment_window, text="Hitung Nilai Rata-rata", command=calculate_average_grade, font=("Arial", 14, "bold"))
    button_calculate.grid(row=8, column=0, columnspan=2, pady=20)

    # Listbox untuk menampilkan data mahasiswa
    students_listbox = Listbox(assessment_window, font=("Arial", 12), width=40, height=5)
    students_listbox.grid(row=9, column=0, columnspan=2, pady=10)

    assessment_window.mainloop()

def open_main_window(nama, nim):
    main_window = Tk()
    main_window.title("Pilih Tipe Nilai")
    main_window.config(bg="lightblue")

    # Calculate the position for the window to be centered
    window_width = 300
    window_height = 200
    screen_width = main_window.winfo_screenwidth()
    screen_height = main_window.winfo_screenheight()
    position_top = int((screen_height - window_height) / 2)
    position_right = int((screen_width - window_width) / 2)
    main_window.geometry(f"{window_width}x{window_height}+{position_right}+{position_top}")

    # Configure grid layout
    main_window.columnconfigure(0, weight=1)

    # Welcome Label
    label_welcome = Label(main_window, text=f"Selamat datang, {nama}!", font=("Arial", 14), bg="lightblue")
    label_welcome.grid(row=0, column=0, pady=10)

    # Buttons to choose assessment type
    button_tugas = Button(main_window, text="Hitung Rata-Rata Tugas", command=lambda: [main_window.withdraw(), open_assessment_window(nama, nim, "Tugas", main_window)], font=("Arial", 12))
    button_tugas.grid(row=1, column=0, pady=5)

    button_uts = Button(main_window, text="Hitung Rata-Rata UTS", command=lambda: [main_window.withdraw(), open_assessment_window(nama, nim, "UTS", main_window)], font=("Arial", 12))
    button_uts.grid(row=2, column=0, pady=5)

    button_uas = Button(main_window, text="Hitung Rata-Rata UAS", command=lambda: [main_window.withdraw(), open_assessment_window(nama, nim, "UAS", main_window)], font=("Arial", 12))
    button_uas.grid(row=3, column=0, pady=5)

    main_window.mainloop()

def login():
    nama = entry_login_name.get()
    nim = entry_login_nim.get()

    # Basic validation for non-empty fields
    if nama and nim:
        login_window.destroy()
        open_main_window(nama, nim)
    else:
        messagebox.showerror("Error", "Nama dan NIM harus diisi!")

# Login Window
login_window = Tk()
login_window.title("Login Mahasiswa")
login_window.config(bg="lightblue")

# Calculate the position for the login window to be centered
login_window_width = 350
login_window_height = 200
screen_width = login_window.winfo_screenwidth()
screen_height = login_window.winfo_screenheight()
position_top = int((screen_height - login_window_height) / 2)
position_right = int((screen_width - login_window_width) / 2)
login_window.geometry(f"{login_window_width}x{login_window_height}+{position_right}+{position_top}")

# Configure grid layout
login_window.columnconfigure(0, weight=1)
login_window.columnconfigure(1, weight=1)

# Login Labels and Entries
label_login_name = Label(login_window, text="Nama Mahasiswa:", font=("Arial", 12), bg="lightblue")
label_login_name.grid(row=0, column=0, sticky=E, padx=10, pady=10)
entry_login_name = Entry(login_window, font=("Arial", 12), width=20)
entry_login_name.grid(row=0, column=1, sticky=W, padx=10, pady=10)

label_login_nim = Label(login_window, text="NIM:", font=("Arial", 12), bg="lightblue")
label_login_nim.grid(row=1, column=0, sticky=E, padx=10, pady=10)
entry_login_nim = Entry(login_window, font=("Arial", 12), width=20)
entry_login_nim.grid(row=1, column=1, sticky=W, padx=10, pady=10)

# Login Button
button_login = Button(login_window, text="Login", command=login, font=("Arial", 14, "bold"))
button_login.grid(row=2, column=0, columnspan=2, pady=20)

login_window.mainloop()
