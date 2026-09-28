from cryptography.fernet import Fernet
import base64

SECRET_KEY = base64.urlsafe_b64encode(b'01234567890123456789012345678901')

def encrypt_process():
    print("\n--- Encryption ---")
    message = input("Encrypt: ")
    date_str = input("Enter thedate(EX- 1970-09-28): ")
    
    f = Fernet(SECRET_KEY)
    combined_data = f"{date_str}|{message}"
    encrypted_message = f.encrypt(combined_data.encode())
    
    print("\n[✔] Here is your encrypted code.:")
    print(encrypted_message.decode())

def decrypt_process():
    print("\n--- Decryption ---")
    encrypted_text = input("Decrypt: ").strip()
    input_date = input("nter thedate(EX- 1970-09-28)): ").strip()
    
    f = Fernet(SECRET_KEY)
    try:
        decrypted_bytes = f.decrypt(encrypted_text.encode())
        decrypted_text = decrypted_bytes.decode()
        
        saved_date, original_message = decrypted_text.split("|", 1)
        
        if saved_date == input_date:
            print(f"Original message: {original_message}")
        else:
            print(f"\n[❌]")
            
    except Exception as e:
        print(f"\n[❌].")

if __name__ == "__main__":
    print("========================================")
    print("1. Encryption")
    print("2. Decryption")
    
    choice = input("\n What do you need to do?: ").strip()
    
    if choice == '1':
        encrypt_process()
    elif choice == '2':
        decrypt_process()
    else:
        print("\n[!] ")
