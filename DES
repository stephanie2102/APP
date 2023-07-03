from cryptography.fernet import Fernet
from tkinter import Tk, Label, Entry, Button, filedialog

class FileEncryptionApp:
    def __init__(self):
        self.root = Tk()
        self.root.title("Cifrador de Archivos")
        
        self.file_path = None
        self.key = None
        
        self.message_label = Label(self.root, text="Mensaje:")
        self.message_label.pack()
        
        self.message_entry = Entry(self.root, width=50)
        self.message_entry.pack()
        
        self.key_label = Label(self.root, text="Clave (8 caracteres):")
        self.key_label.pack()
        
        self.key_entry = Entry(self.root, width=20)
        self.key_entry.pack()
        
        self.encrypt_button = Button(self.root, text="Cifrar", command=self.encrypt_file)
        self.encrypt_button.pack()
        
        self.load_button = Button(self.root, text="Cargar Archivo Cifrado", command=self.load_encrypted_file)
        self.load_button.pack()
        
        self.decrypt_label = Label(self.root, text="Archivo Cifrado:")
        self.decrypt_label.pack()
        
        self.decrypt_entry = Entry(self.root, width=50)
        self.decrypt_entry.pack()
        
        self.decrypt_button = Button(self.root, text="Descifrar", command=self.decrypt_file)
        self.decrypt_button.pack()
        
    def encrypt_file(self):
        message = self.message_entry.get()
        self.key = self.key_entry.get().encode()
        
        fernet = Fernet(self.key)
        encrypted_message = fernet.encrypt(message.encode())
        
        file_path = filedialog.asksaveasfilename(defaultextension=".txt")
        with open(file_path, 'wb') as file:
            file.write(encrypted_message)
        
        self.file_path = file_path
        self.decrypt_entry.delete(0, 'end')
        self.decrypt_entry.insert(0, self.file_path)
        
    def load_encrypted_file(self):
        file_path = filedialog.askopenfilename(filetypes=[("Text Files", "*.txt")])
        self.file_path = file_path
        self.decrypt_entry.delete(0, 'end')
        self.decrypt_entry.insert(0, self.file_path)
        
    def decrypt_file(self):
        if self.file_path is None:
            return
        
        self.key = self.key_entry.get().encode()
        
        fernet = Fernet(self.key)
        with open(self.file_path, 'rb') as file:
            encrypted_message = file.read()
        
        decrypted_message = fernet.decrypt(encrypted_message).decode()
        
        self.message_entry.delete(0, 'end')
        self.message_entry.insert(0, decrypted_message)
        
    def run(self):
        self.root.mainloop()


app = FileEncryptionApp()
app.run()
