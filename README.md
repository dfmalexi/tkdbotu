# tkdbotu
Kelimenin Türkçe olup olmadığını kontrol eder.
tkdbotu.py programdır.
import sys
kalin_ünlü = ["a", "ı", "o", "u"]
ince_ünlü = ["e", "i", "ö", "ü"]
ünlü = ["e", "i", "ö", "ü", "a", "ı", "o", "u"]
düz_ünlü = ["a", "e", "ı", "i"]
yuvarlak_ünlü = ["o", "ö", "u", "ü"]
yuvarlak_dar = ["u", "ü"]
düz_geniş = ["a", "e"]
result = ""
art_ünlü = ["a", "ı", "o", "u"]
ön_ünlü = ["e", "i", "ö", "ü"]
acik_ünlü = ["a", "e", "o", "ö"]
kapali_ünlü = ["ı", "i", "u", "ü"]
tonlu_ünsüzler = ["b", "c", "d", "g", "ğ",
                  "j", "l", "m", "n", "r", "v", "y", "z"]
tonsuz_ünsüzler = ["ç", "f", "h", "k", "p", "s", "ş", "t"]
genis_ünlü = ["a", "o", "e", "ö"]
dar_ünlü = ["ı", "u", "i", "ü"]
#oluşum yerlerine göre
dudak_unsuzleri=["b","m","p"]
diş_ünsüzleri=["d","n","s","t","z"]
diş_dudak_ünsüzleri=["f","v"]
diş_damak_ünsüzleri=["c","ç","j","ş"]
ön_damak_ünsüzleri=["r,y"]
hem_ön_hem_art_ünsüzleri=["g","k","l"]
art_ünsüzleri=["ğ"]
gırlak_ünsüzleri=["h"]
#sürekli ünsüzler
sızıcı_ünsüzler=["f","ğ","h","j","s","ş","v","z"]
akıcı_ünsüzler=["l","m","n","r","y"]
#süreksiz ünsüzler
süreksiz_ünsüzler=["b","c","ç","d","g","k","p","t"]


def check_ton(kelime):
    print("Checking ton:".center(50, "-"))
    for i in kelime:
        if i in ünlü:
            print(f"{i} : tonlu'dur.")
        elif i in tonlu_ünsüzler:
            print(f"{i} : tonlu'dur.")
        elif i in tonsuz_ünsüzler:
            print(f"{i} : tonsuzdur.")
        else:
            print(f"{i} : sistem düzgün çalışmadı")


def check_rule1(kelime):
    result = ""
    print("checking artlık-önlük rule-1".center(50, "-"))
    for i in kelime:
        if i in art_ünlü:
            if result == "":
                result = "a"
            elif result == "a":
                pass
            else:
                print("art ünlü kurulına uymaz")
        elif i in ön_ünlü:
            if result == "":
                result = "ö"
            elif result == "ö":
                pass
            else:
                print("ön ünlüye uymaz")


def check_rule2(kelime):
    result = "d"
    print("checking dudak uyumu rule-2".center(50, "-"))
    for i in kelime:
        if i in ünlü:
            if i in düz_ünlü:
                if result == "":
                    result = "d"
                elif result == "d":
                    pass
                else:
                    if i in düz_geniş:
                        result = "d"
                    else:
                        print("yuvarlaktan sonra düz geniş gelmemiş.")
            else:
                if result == "d":
                    print("düzden sonra düz gelmeli uymaz.")
                elif result == "":
                    result = "y"
                else:
                    if i == yuvarlak_dar:
                        pass
                    else:
                        print("yuvarlaktan sonra yuvarlak dar gelmemiş.")


def düzlük_yuvarlaklik(kelime):
        print("checking düz yuvarlaklık".center(50,"-"))
        for i in kelime:
            if i in ünlü:
                if i in genis_ünlü:
                    if i in düz_geniş:
                        if i in art_ünlü:
                            print(f"{i} : art ünlü düz ve geniştir.")
                        else:
                            print(f"{i} : ön ünlü düz ve geniştir.")
                    else:
                        if i in art_ünlü:
                            print(f"{i} : art ünlü yuvarlak ve geniştir.")
                        else:
 
                            print(f"{i} : ön ünlü yuvarlak ve geniştir.")
 #dar
                else:
                    if i in düz_ünlü:
                        if i in art_ünlü:
                            print(f"{i} : art ünlü düz ve dar'dır.")
                        else:
                            print(f"{i} : ön ünlü düz ve dar'dır.")

                    else:
                        if i in art_ünlü:
                            print(f"{i} : art ünlü yuvarlak ve dar'dır.")
                        else:
                            print(f"{i} : ön ünlü yuvarlak ve dar'dır.")

def check_ünsüz(kelime):
    print("checking oluşum yerlerine göre ünsüzler".center(50,"-"))
    for i in kelime:
        if i in dudak_unsuzleri:
            print(f"{i} : ünsüzü dudak ünsüzüdür.")
        elif i in diş_ünsüzleri:
            print(f"{i} : ünsüzü diş ünsüzüdür.")
        elif i in diş_dudak_ünsüzleri:
            print(f"{i} : ünsüzü diş dudak ünsüzüdür.")
        elif i in diş_damak_ünsüzleri:
            print(f"{i} : ünsüzü diş damak ünsüzüdür.")
        elif i in ön_damak_ünsüzleri:
            print(f"{i} : ünsüzü ön damak ünsüzüdür.")
        elif i in art_ünsüzleri:
            print(f"{i} : ünsüzü art damak ünsüzüdür.")
        elif i in gırlak_ünsüzleri:
            print(f"{i} : ünsüzü gırtlak ünsüzüdür.")
        elif i in hem_ön_hem_art_ünsüzleri:
            print(f"{i} : ünsüzünü oku normal bir ses varsa ön boğazdan bir ses varsa art.")
def sürekli_süreksiz_ünsüzler(kelime):
    print("checking sürekli süreksiz".center(50,"-"))
    for i in kelime:
        if i in sızıcı_ünsüzler:
            print(f"{i} : ünsüzü sürekli ve sızıcı ünsüzdür.")
        elif i in akıcı_ünsüzler:
            print(f"{i} : ünsüzü sürekli ve akıcı ünsüzüdür.")
        elif i in süreksiz_ünsüzler:
            print(f"{i} : ünsüzü süreksiz ünsüzüdür.")
def agız_geniz(kelime):
    print("checking ağız geniz".center(50,"-"))
    for i in kelime:
        if i in ["m","n"]:
            print(f"{i} : ünsüzü geniz ünsüzüdür.")
        else:
            if i not in ünlü:
                print(f"{i} : ünsüzü ağız ünsüzüdür.")
            
print("kelimeyi giriniz".center(50, "*"))
for line in sys.stdin:

    for i in line:
        for y in ünlü:
            if i == y:
                if i in kalin_ünlü:
                    if result != "i":

                        result = "k"
                    else:
                        print("Büyük ünlüye uymaz")
                        break
                else:
                    if result != "k":
                        result = "i"
                    else:
                        print("Büyük ünlüye uymaz")
                        break
    result = ""
    for i in line:
        for y in ünlü:
            if i == y:
                if i in düz_ünlü:
                    if result == "d":
                        pass
                    elif result == "y":
                        if i in düz_geniş:
                            result = "d"
                        else:
                            print("küçük ünlüye uymaz")
                    else:
                        result = "d"

                else:
                    if result == "y":
                        if i in yuvarlak_dar:
                            result = "y"
                        else:
                            print("küçük ünlüye uymaz.")
                    elif result == "d":
                        print("Küçük ünlüye uymaz.")
                    else:
                        result = "y"
    check_ton(line.strip())
    check_rule1(line.strip())
    check_rule2(line.strip())
    düzlük_yuvarlaklik(line.strip())
    check_ünsüz(line.strip())
    sürekli_süreksiz_ünsüzler(line.strip())
    agız_geniz(line.strip())
    print("kelimeyi giriniz".center(200, "*"))
