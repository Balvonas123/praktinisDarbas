# praktinisDarbas
kodas galiausiai man suzulo galutinai , taciau tikrinau per C++ compileri jis veikia ir ismeta viska ko praso. kodas zemiau.
#include <iostream>
#include <string>
using namespace std;
 
class Vigenere
{
    public:
        string key;
 
        Vigenere(string key)
        {
            for (int i = 0; i < key.size(); ++i)
            {
                if (key[i] >= 'A' && key[i] <= 'Z')
                    this->key += key[i];
                else if (key[i] >= 'a' && key[i] <= 'z')
                    this->key += key[i] + 'A' - 'a';
            }
        }
 
        string encrypt(string text)
        {
            string out;
 
            for (int i = 0, j = 0; i < text.length(); ++i)
            {
                char c = text[i];
 
                if (c >= 'a' && c <= 'z')
                    c += 'A' - 'a';
                else if (c < 'A' || c > 'Z')
                    continue;
 
                out += (c + key[j] - 2 * 'A') % 32 + 'A';
                j = (j + 1) % key.length();
            }
 
            return out;
        }
 
        string decrypt(string text)
        {
            string out;
 
            for (int i = 0, j = 0; i < text.length(); ++i)
            {
                char c = text[i];
 
                if (c >= 'a' && c <= 'z')
                    c += 'A' - 'a';
                else if (c < 'A' || c > 'Z')
                    continue;
 
                out += (c - key[j] + 32) % 32 + 'A';
                j = (j + 1) % key.length();
            }
 
            return out;
        }
};
 
int main()
{
    Vigenere cipher("VIGENERECIPHER");
 
    string original =
            "Yra ka cia veikti tai gal tiks sitas kodas, perdaug cia laiko !!";
    string encrypted = cipher.encrypt(original);
    string decrypted = cipher.decrypt(encrypted);
 
    cout << original << endl;
    cout << "Encrypted: " << encrypted << endl;
    cout << "Decrypted: " << decrypted << endl;
}
