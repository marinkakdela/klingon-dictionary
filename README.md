# klingon-dictionary
import json

class KlingonDictionary:
    def __init__(self, file_name="klingon_dict.json"):
        self.file_name = file_name
        self.load_data()

    def load_data(self):
        """Load dictionary from file or create a new one."""
        try:
            with open(self.file_name, "r", encoding="utf-8") as file:
                self.words = json.load(file)
        except (FileNotFoundError, json.JSONDecodeError):
            self.words = {}

    def save_data(self):
        """Save dictionary data to a file."""
        with open(self.file_name, "w", encoding="utf-8") as file:
            json.dump(self.words, file, indent=4, ensure_ascii=False)

    def add_word(self, english, klingon):
        """Add a new word to the Klingon dictionary."""
        self.words[english] = klingon
        self.save_data()
        print(f"Added: {english} -> {klingon}")

    def translate(self, english):
        """Translate an English word to Klingon."""
        return self.words.get(english, "Word not found in Klingon dictionary.")

    def list_words(self):
        """List all words in the dictionary."""
        if not self.words:
            print("No words in the dictionary yet.")
            return
        for eng, kling in self.words.items():
            print(f"{eng} -> {kling}")

# Example usage
def main():
    klingon_dict = KlingonDictionary()
    while True:
        print("\nKlingon Dictionary")
        print("1. Add a Word")
        print("2. Translate a Word")
        print("3. List All Words")
        print("4. Exit")
        choice = input("Select an option: ")
        
        if choice == "1":
            english = input("Enter English word: ")
            klingon = input("Enter Klingon translation: ")
            klingon_dict.add_word(english.strip(), klingon.strip())
        elif choice == "2":
            english = input("Enter English word: ")
            print(f"Klingon: {klingon_dict.translate(english.strip())}")
        elif choice == "3":
            klingon_dict.list_words()
        elif choice == "4":
            break
        else:
            print("Invalid choice. Try again.")

if __name__ == "__main__":
    main()
hjhbuui
