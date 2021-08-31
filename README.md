# Super-Smart_Thesaurus
This is a smart user friendly command-line English Thesaurus program that provides you with the definition of any English Word in the world. No matter if the Word has more than One definition, The thesaurus will provide you with all possible definitions of the Word. Incase, you mispelled a Word, the Smart-Thesaurus provides the similar words that may be the word you were actually looking for. It runs an algorithm for choosing which words to suggest to the User so that only those words will be suggested which have 0.8 Ratio Similarity to the Original Word.

import json
from difflib import get_close_matches

data = json.load(open("data.json"))

def translate(w):
    w = w.lower()
    if w in data:
        return data[w]
    elif w.title() in data:
        return data[w.title()]
    elif w.upper() in data:
        return data[w.upper()]        
    elif len(get_close_matches(w, data.keys())) > 0:
        yn = input('Did you mean %s instead? Enter Y if yes, or N if no: ' % get_close_matches(w, data.keys())[0])
        if yn == "Y":
            return data[get_close_matches(w, data.keys())[0]]
        elif yn == "N":
            return "The word doesn't exist. Please double-check it."
        else:
            return "We didn't understand your entry."   
    else:
        return "The word doesn't exist. Please double-check it"    

word = input("Enter word: ")

output = translate(word)
if type(output) == list:
    for item in output:
        print(item)
else:
    print(output)
