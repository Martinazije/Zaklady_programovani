import sys
import json
import pdb

#Nacteni vstupnich argumentu (vstupni a vystupni soubor)
if len(sys.argv)>2:
    data_import=sys.argv[1]
    data_export=sys.argv[2]
else:
    print("Nedostatecny pocet vstupnich argumentu!")
    data_import='stromy.geojson'
    data_export='export.geojson'
    print('Argumenty nastaveny na "stromy.geojson" a "export.geojson".')


# nacteni geojsonu
with open(data_import, encoding='utf-8') as f:
    f = json.load(f)

# vytvoreni seznamu a nacteni souradnic do neho
data = []
i = -1
for feature in f['features']:
    i = i + 1
    data.append(feature['geometry']['coordinates'])
    data[i].append(0)

#zjisteni stredovych souradnic
def get_x_half(data):
    xmin = min(x[0] for x in data)
    xmax = max(x[0] for x in data)
    return (xmax - xmin) / 2 + xmin


def get_y_half(data):
    ymin = min(y[1] for y in data)
    ymax = max(y[1] for y in data)
    return (ymax - ymin) / 2 + ymin


#vypocte osy, podle kterych se bude delit
half_x = get_x_half(data)
half_y = get_y_half(data)


# rozdeleni bodu podle stredovych souradnic a prirazeni identifikatoru
def rozrazeni(data, half_x, half_y):
    #kontrola, zdali vstup uz neobsahuje mene nez 50 bodu
    if len(data)<=50:
        return data

    # vytvoreni 4 seznamu
    sektor1 = []
    sektor2 = []
    sektor3 = []
    sektor4 = []

    # zjisteni jejich polohy a prirazeni ID clusteru
    i = -1
    for feature in data:
        i = i + 1
        x = data[i][0]
        y = data[i][1]
        if x < half_x and y > half_y:
            data[i][2] = str(data[i][2]) + '1'
            sektor1.append(feature)
        elif x > half_x and y > half_y:
            data[i][2] = str(data[i][2]) + '2'
            sektor2.append(feature)

        elif x < half_x and y < half_y:
            data[i][2] = str(data[i][2]) + '3'
            sektor3.append(feature)

        elif x > half_x and y < half_y:
            data[i][2] = str(data[i][2]) + '4'
            # pdb.set_trace()
            sektor4.append(feature)

    #pokud sektor1,2,3,4 obsahuje vice nez 50 bodu, dochazi k novemu deleni a prirazovani ID
    if len(sektor1) > 50:
        half_x = get_x_half(sektor1)
        half_y = get_y_half(sektor1)
        sektor1=rozrazeni(sektor1, half_x, half_y)
    if len(sektor2) > 50:
        half_x = get_x_half(sektor2)
        half_y = get_y_half(sektor2)
        sektor2=rozrazeni(sektor2, half_x, half_y)
    if len(sektor3) > 50:
        half_x = get_x_half(sektor3)
        half_y = get_y_half(sektor3)
        sektor3=rozrazeni(sektor3, half_x, half_y)
    if len(sektor4) > 50:
        half_x = get_x_half(sektor4)
        half_y = get_y_half(sektor4)
        sektor4=rozrazeni(sektor4, half_x, half_y)

    data=sektor1+sektor2+sektor3+sektor4
    return data

# a proto jdou do metody dump na poslednim radku prave data (ne data_after)
data_after=rozrazeni(data,half_x, half_y)

with open(data_export, 'w') as g:
    json.dump(data,g)
