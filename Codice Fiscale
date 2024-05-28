from bs4 import BeautifulSoup as BS
from os import system

class CodiceFiscale:
    def __init__(self) -> None:
        self.CodiceFiscale = self.GenerareCodiceFiscale()
        return None
    def GenerareCodiceFiscale(self) -> str:
        def Posizioni1_3() -> str:
            Cognome = input("Inserire il cognome: ").replace(" ", "")
            while not Cognome.isalpha():
                print("Cognome non valido")
                Cognome = input("Inserire il cognome: ").replace(" ", "")
            ans, Cognome = "", Cognome.upper()
            vowels = ("A", "E", "I", "O", "U")
            for ch in Cognome:
                if ch not in vowels:
                    ans += ch
                    if len(ans) == 3:
                        return ans
            for ch in Cognome:
                if ch in vowels:
                    ans += ch
                    if len(ans) == 3:
                        return ans
            while len(ans) < 3:
                ans += "X"
            return ans
        def Posizioni4_6() -> str:
            Nome = input("Inserire il nome: ").replace(" ", "")
            while not Nome.isalpha():
                print("Nome non valido")
                Nome = input("Inserire il nome: ").replace(" ", "")
            ans, Nome = "", Nome.upper()
            Consonants = [ch for ch in Nome if ch not in ("A", "E", "I", "O", "U")]
            if len(Consonants) > 3:
                return Consonants[0] + Consonants[2] + Consonants[3]
            for ch in Consonants:
                ans += ch
                if len(ans) == 3:
                    return ans
            Vowels = [ch for ch in Nome if ch in ("A", "E", "I", "O", "U")]
            for ch in Vowels:
                ans += ch
                if len(ans) == 3:
                    return ans
            while len(ans) < 3:
                ans += "X"
            return ans
        def Posizioni7_11() -> str:
            #Controllo input
            Giorno_nascita = input("Inserire il giorno di nascita: ").replace(" ", "")
            while not Giorno_nascita.isdigit() or int(Giorno_nascita) == 0 or int(Giorno_nascita) > 31:
                print("Giorno non valido, Inserire un valore compreso tra 1 e 31")
                Giorno_nascita = input("Inserire il giorno di nascita: ").replace(" ", "")
            Giorno_nascita = int(Giorno_nascita)

            Mese_nascita = input("Inserire il mese di nascita: ").replace(" ", "")
            while not Mese_nascita.isdigit() or int(Mese_nascita) == 0 or int(Mese_nascita) > 12:
                print("Mese non valido, Inserire un valore compreso tra 1 e 12")
                Mese_nascita = input("Inserire il mese di nascita: ").replace(" ", "")
            Mese_nascita = int(Mese_nascita)

            Anno_nascita = input("Inserire l'anno di nascita: ").replace(" ", "")
            while not Anno_nascita.isdigit() or int(Anno_nascita) < 1000 or int(Anno_nascita) > 2024:
                print("Anno non valido")
                Anno_nascita = input("Inserire l'anno di nascita: ").replace(" ", "")
            Sesso = input("Inserire il proprio sesso: ").replace(" ", "")
            while not Sesso.isalpha() or (Sesso.upper() != "M" and Sesso.upper() != "F"):
                print("Sesso non valido")
                Sesso = input("Inserire il proprio sesso: ").replace(" ", "")
            Sesso = Sesso.upper()
            #Posizione 7-8
            ans = Anno_nascita[2:4]

            #Posizione 9
            arr = ["A", "B", "C", "D", "E", "H", "L", "M", "P", "R", "S", "T"]
            ans += arr[Mese_nascita-1]

            #Posizione 10-11
            if Sesso == "M":
                if Giorno_nascita < 10:
                    ans += "0" + str(Giorno_nascita)
                else:
                    ans += str(Giorno_nascita)
            else:
                ans += str(Giorno_nascita + 40)
            return ans
        
        def Posizioni12_15() -> str:
            comune = input("Inserire il comune di nascita: ").upper()
            while not comune.isalpha():
                print("Comune non valido")
                comune = input("Inserire il nome: ").upper()

            #Cittadino italiano
            with open(r"Comuni.html", "r") as file:
                soup = BS(file, features="lxml")
                tr = soup.find("td", string=comune)
                if tr:
                    tr= tr.find_next_siblings()
                    if tr:
                        ans = tr[-1].text
                        return ans
            
            #Cittadino straniero
            with open(r"Comuni EE.html", "r") as file:
                soup = BS(file, features="lxml")
                tr = soup.find("td", string=comune)
                if tr:
                    tr= tr.find_next_siblings()
                    if tr:
                        ans = tr[0]
                        if ans:
                            return ans.text
            #Caso di errore
            print("Comune non trovato, verifichi che sia scritto bene")
            return Posizioni12_15()
        def Posizione16(codice):
            s = 0
            #numeri dispari che considero come pari perché inizio dal index 0
            with open(r"CaratteriPari.html", "r") as file:
                soup = BS(file, features="lxml")
                for i in range(0, len(codice), 2):
                    letter = soup.find("b", string = codice[i])
                    if letter:
                        letter = letter.find_parent()
                        if letter:
                            letter = letter.find_next_sibling()
                            if letter:
                                s += int(letter.text)
            #numeri pari che considero dispari
            for i in range(1, len(codice), 2):
                if codice[i].isdecimal():
                    s += int(codice[i])
                else:
                    s += ord(codice[i]) - 65
            #resto
            with open(r"Resto.html", "r") as file:
                soup = BS(file, features="lxml")
                ans = soup.find("b", string = str(s%26))
                if ans:
                    ans = ans.find_parent()
                    if ans:
                        ans = ans.findNextSibling()
                        if ans:
                            return ans.text
            return ""
        Codice = Posizioni1_3()
        Codice += Posizioni4_6()
        Codice += Posizioni7_11()
        Codice += Posizioni12_15()
        Codice += Posizione16(Codice)
        return Codice

if __name__ == "__main__":
    system("cls")
    obj = CodiceFiscale()
    print(obj.CodiceFiscale)
