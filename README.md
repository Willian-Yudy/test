#include <iostream>
#include <string>
using namespace std;

class Book {
private:
    string title;
    string author;
    string isbn;
    bool available;

public:
    void setBookDetails(string t, string a, string i, bool avail) {
        title = t;
        author = a;
        isbn = i;
        available = avail;
    }

    void displayBookDetails() {
        cout << "Título: " << title << endl;
        cout << "Autor: " << author << endl;
        cout << "ISBN: " << isbn << endl;
        cout << "Disponibilidade: " << (available ? "Disponível" : "Emprestado") << endl;
        cout << "---------------------------" << endl;
    }

    bool borrowBook() {
        if (available) {
            available = false;
            return true;
        }
        return false;
    }

    void returnBook() {
        available = true;
    }

    string getISBN() {
        return isbn;
    }

    bool isAvailable() {
        return available;
    }
};

int main() {
    Book library[5];

    // Inicializando os livros que temos na biblioteca do sistema 
    library[0].setBookDetails("Freakonomics", "Steven D. Levitt & Stephen J. Dubner", "006073132X", true);
    library[1].setBookDetails("O Andar do Bêbado", "Leonard Mlodinow", "8535916814", true);
    library[2].setBookDetails("A Riqueza das Nações", "Adam Smith", "8572329226", true);
    library[3].setBookDetails("Crash: Uma Breve História da Economia", "Alexandre Versignassi", "8577020487", false); // já emprestado para alguem
    library[4].setBookDetails("O Capital no Século XXI", "Thomas Piketty", "853591126X", true);

    string inputISBN;
    cout << "=== Alex's Library ===" << endl;

    while (true) {
        cout << "\nLivros disponíveis:\n";
        for (int i = 0; i < 5; i++) {
            library[i].displayBookDetails();
        }

        cout << "Digite o ISBN do livro que deseja emprestar (ou 0 para sair): ";
        getline(cin, inputISBN);

        if (inputISBN == "0") {
            cout << " Sistema encerrado. Até a próxima!" << endl;
            break;
        }

        bool found = false;
        for (int i = 0; i < 5; i++) {
            if (library[i].getISBN() == inputISBN) {
                found = true;
                if (library[i].isAvailable()) {
                    library[i].borrowBook();
                    cout << "✅ Livro emprestado com sucesso!" << endl;
                }
                else {
                    cout << "❌ Este livro já está emprestado." << endl;
                }
                break;
            }
        }

        if (!found) {
            cout << "❌ Livro com ISBN " << inputISBN << " não encontrado." << endl;
        }
    }

    return 0;
}

