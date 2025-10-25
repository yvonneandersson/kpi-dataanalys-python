# 📊 Data Analysis in Python

This repository contains a Python project where the assignment focuses on building a structured and interactive data analysis tool that examines **Consumer Price Index (CPI)** and price trends across various categories from 1980 to 2022.

The application uses CSV files containing real statistical data from SCB (Statistics Sweden), and enables users to visualize and explore economic trends using a menu-driven terminal interface.

---

## 🎯 Objective

- Practice modular and functional Python programming.
- Analyze real-world economic data from CSV files.
- Create clear and informative plots using `matplotlib`.
- Apply programming best practices: readable code, meaningful variable names, and clear documentation of intent.

---

## 🧱 Features & Structure

- 📁 **CSV Input**: Load data from `kpi.csv`, `livsmedel.csv`, and `tjanster.csv`.
- 📈 **Visualization**:
  - Line and bar plots of KPI trends (1980–2022).
  - Price development of goods and services (1980–2021).
  - Scatter plot highlighting highest and lowest annual CPI values.
- 📊 **Data Computation**:
  - Total, average, min, and max values.
  - Percentage change in prices over time.
- 🔘 **Interactive Menu**:
  - CLI-based interface with 6 options.
  - Options dynamically expand as functionality grows through different assignments.

---

## 🖥 Results + Code (Swedish):

![](https://i.imgur.com/rR5Crlk.png)
![](https://i.imgur.com/Fvwnv03.png)
![](https://i.imgur.com/jiw0Pv7.png)
![](https://i.imgur.com/VtdE3WQ.png)
![](https://i.imgur.com/8SyhBEd.png)
![](https://i.imgur.com/wMli7gA.png)
![](https://i.imgur.com/lBX0SvC.png)
![](https://i.imgur.com/4YUq5y5.png)
![](https://i.imgur.com/mvi5xy6.png)
![](https://i.imgur.com/Q7zEld5.png)
![](https://i.imgur.com/E1RSmUl.png)
![](https://i.imgur.com/t7X9hMY.png)

---

### 👾 Code below:

```python
import matplotlib.pyplot as plt
import csv
###############- Deluppgift 1 -###############
## Följande funktioner för deluppgift 1:
# Denna funktion har modifierads för att passa de olika syftena.
def mean_list(a_list):
    new_list = []
    
    for i, row in enumerate(a_list):
        temp_list = [] #skapar en temporär lista för lägga i de näst kommande beräknade värden.
        
        for kolumn in row:
            temp_list.append(kolumn)
        
        #if i == 0: #rad 0: lägger in stringen medelvärde.
        #temp_list.append('Medelvärde: ')
        else:
            x = 0
            for value in temp_list[1:]: #behövs göras en loop för att exkl. index 0 i kolumnerna och använda resterande värden för beräkning.
                x += float(value)
            means = x/(len(temp_list)-1) #formel för att beräkna medelvärdet
            temp_list.append(round(means, 2)) #för att göra det snyggare med färre deciaml, samt lägger till värdena för medelvärdet för varje rad.
        
        new_list.append(temp_list) #återkommer till den första variabeln ifunktionen, och lägger till för att sedan...
        
    return new_list #... retunera när man anropar funktionen.
    
def sum_list(a_list):
    new_list = [] #en lista att lägga till den temporära listan i.
    for i, row in enumerate(a_list): #räknar upp elementena i rader i listan förparametern.
        temp_list = [] #skapar en temporär lista för beräkningar.
        for kolumn in row:
            temp_list.append(kolumn) #-"-
        
        if i == 0:
            temp_list.append('Radsumma') #rubriken gör det tydligt på rad index 0 för att det är summan som ska beräknas.
        
        else:
            sum = 0
            for value in temp_list[1:]: #använder indexering för att undvika få med kolumnen för årtal i beräkningar
                sum += float(value)
                temp_list.append(round(sum, 2)) #-"-
                new_list.append(temp_list) #-"-
                new_list_all = new_list[0][13], new_list[1][13], new_list[2][13], new_list[3][13], new_list[4][13], new_list[5][13], new_list[6][13], new_list[7][13],new_list[8][13], new_list[9][13], new_list[10][13]
            return new_list_all #efter funktions-beräkningar retunerar man indexet där beräkningarna blev placerade.

##################-Minsta värde-##################
def minValue(a_list): #Beräknar minsta värdet och lägger till index-postion, allt läggs till i en ny lista.
    new_list = []
    for i, row in enumerate(a_list): #går igenom varje element i listan samt index-positionen.
        minValue = min(row)
        minIndex = row.index(minValue)
        new_list.append((minValue, minIndex))
    return new_list

##################-Största värde-##################
def maxValue(a_list): #Fungerar på samma sätt som funktionen minValue, men för max-värdet.
    new_list = []
    for i, row in enumerate(a_list):
        maxValue = max(row)
        maxIndex = row.index(maxValue)
        new_list.append((maxValue, maxIndex))
    return new_list
# Extra hjälp-funktion: Använde mig i detta fall av denna funktion för att beräkna värdena i tabell-diagrammen (menyalt. 4).
def mean(data_csv):

    sum = 0
    for value in data_csv:
        sum += float(value)
        means = sum/len(data_csv)
        x = means
    return x
    
###############- Deluppgift 2 -###############
## Följande funktioner för deluppgift 2:
# Funktion som läser in csv-fil som inargument och används i menyalt. 1 för att läsa in och spara varibel med filen när programmet exekverats.
def readFile(data_csv): #funktion med inargument av excel-fil, som läser in filen och lägga till varje element i 2D-listan i en ny lista.
    data_list = [] #tom lista för lägga till data i CSV-filerna.
    with open(data_csv, 'r', encoding = 'utf-8') as file: #öppnar samt läser filerna för att kunna "kopiera" lägga till.
        csv_text = csv.reader(file, delimiter=';') # "svenska" excel-filer använder oftast ";" som seperation, och behövs göra tydligt iPython för att göra seperationen.
        for rad in csv_text:
            data_list.append(rad)
        
    return data_list

################-Pythonlista: Prisutvecklingen för olika kategorier-
################
# Designar och skapar en tabell med beräknat medelvärde och totala prisutvecklingen för en csv-fil som inargumentet när funktionen anropas.
def MeanAndTotal(data_csv):
#Varibler som är tillför att designa tabellen för argumentet.
    
    str_1 = '+------------------------------------------+-----------+---------------+'
    str_2 = '+==========================================+===========+===============+'
    rubrik = ''
#Inargumentet avgör vad rubriken blir.
    if data_csv == tjansteData:
        rubrik = 'av varor och tjänster'
    elif data_csv == livsmedelData:
        rubrik = 'av livsmedel'
# Skriver ut början av tabellen med tillhörande variabel "rubrik" för CSV-filen.
    print(f'\nPrisutvecklingen för olika kategorier {rubrik} år 1980-2021\
    n{str_1}')
    print(f'|Kategorier {rubrik:<21} {"|Medelvärde |":>22} {"Totalt |":>15}\
    n{str_2}')
# Foor-loop exkl. årtalen, med numeriska-stringvärden omvandlat till float samt kategorierna som senare ska tillämpas i tabellen.
    for num in data_csv[1:]:
        kategori = num[0]
        rowValues = ([float(value) for value in num[1:]])
# Beräknade värdet för resp. medel- och tot-värdet läggs in tillsammans med det tillhörandet året och går igenom tills alla värden har gått igenom.
        means = (mean(rowValues[1:]))
        tot = ((rowValues[-1]-rowValues[0]))
        print(f'|{kategori:<42}|{means:11.2f}|{tot:15.2f}|\n{str_1}')
###############- Deluppgift 3: Plotta grafen -
###############
def plotta_data(data_csv):
#Listar följande färger för att plotta linjerna samt färgindex som går igenom listan och applicerar på respektive linje.
    colors = ['blue', 'orange', 'green', 'red', 'purple', 'brown', 'pink', 'black']
    colorIndex = 0 #Används som startvärde och för att kunna öka och kommer blir är kopplat som index till "colors".
#List-comprehension, för att omvandla första raden till float värden som är årtalen (x-värden) och skippar index 0, eftersom det endast är blank.
    xValues = [float(row) for row in data_csv[0][1:]]
#for-loop som sparar titlarna/rubrikerna i en variabel i kolumn 1 samt konverterad y-värden för resterande rader och kolumner som läggs i seperate listor för varje kolumn (dvs årtal).

    for row in data_csv[1:]:
        header = row[0]
        yValues = ([float(value) for value in row[1:]])
#Läser in följande CSV-fil och tillhörande kategori som ska används som "label" när grafen plottas.
        if data_csv == livsmedelData:
            kategori = 'livsmedel'
            plt.plot(xValues, yValues, color = colors[colorIndex], label = header)
#-''-
        elif data_csv == tjansteData:
            kategori = 'kategorier av varor och tjänster'
            plt.plot(xValues, yValues, color = colors[colorIndex], label = header)
        colorIndex +=1 #Efter varje plottad koordinat, ökar färgindex med 1, vilket innebär att positionen för listan "colors" ökar och går därmed igenom listan och lägger till en ny färg för nästa koordinat.
#Grafen med titlar för x och y och huvudrubrik samt utseende och placering för etikett.
    plt.title(f'Prisutvecklingen för olika {kategori} År 1980-2021') #f-string för att kunna hantera variabelen "kategori", varibeln beror på argumentet.
    plt.xlabel('År')
    plt.ylabel('Prisutvecklingen')
    plt.grid()
    plt.legend(fontsize = 'x-small', loc = 'upper left')
    plt.show()
###############- Deluppgift 4: Medelvärde för kpiData -###############
def staphleDiagram(data_csv, month):
#Tomma listor för att implementera samtliga x- och y-värden och annan data för beräkning.
    xData, data2, redData, x_Values2021, x_Values2022, y_Lists, headers = [],[],[],[],[],[],[] #Uppdaterade för mindre kod.
## xData skriver ut alla värden som tillhör resp. år, data2 skriver ut värden för varje tillhörande år.
    xData.append([[float(val) for val in row[0:]] for row in data_csv[1:]]) #jan-juli 2022-1980
    data2.append([[float(val) for val in row[1:]] for row in data_csv[1:]]) #aug-dec fr 2021-1980
    redData.append(([[float((val)) for val in row[8:]] for row in data_csv[2:]]))
# y- och x-värden för respek. rad genom att använda list comprehension för mindre kod.
    xData = [int(row[0]) for row in xData[0]] # x-värden
    data2 = [row[0:] for row in data2[0]] # y-värden
    redData = [row[0:] for row in redData[0]] # x-värden fr.o.m augsti 2021
# Medelvärde för y-koordinaterna för jan-juli (2022-1980) och aug-dec (2021-1980)
    y_Means21 = []
    y_Means21 = [x[-1] for x in (mean_list(data2))] #modifierade mean_list för att passa detta behov.
# Medelvärde för resp. månad Jan-Jul fr.o.m 2022 (röda linjen)
    y_valuesRed1 = []
    for i in range(len(data2[0])):
        row_values = [row[i] for row in data2]
        y_valuesRed1.append(row_values)
    
    y_meansRed1 = [x[-1] for x in mean_list(y_valuesRed1)] #anropar tidigare funktion för medelvärdet, och får medelvärdet i sista index för varje lista.
# Medelvärde för resp. månad Aug-Dec för varje årtal fr.o.m 2021 (röda linjen)
    y_valuesRed2 = []
    for i in range(len(redData[0])):
        row_values = [row[i] for row in redData[0:]]
        y_valuesRed2.append(row_values)
    y_meansRed2 = [x[-1] for x in mean_list(y_valuesRed2)] #-''-
# User-input för resp. månad (röd linje)
    y_valuesRed_1_2 = [None] + y_valuesRed1 + y_valuesRed2 #indexerar 0 med värdet None för att det ska stämma med user_input och att rätt värden kommer fram för denne input.
    label = [None] + ['januari', 'februari', 'mars', 'april', 'maj', 'juni','juli', ' augusti', ' september', ' oktober', ' november', ' december']
# (Gäller jan-aug t.o.m 2022)
# Beroende på vilken input från användaren (month), där month motsvarar indexet för det beräknade medelvärdet, som därefter sparars i en variabel och plottas utefter det tillsammans det redan beräknade x-värdena i en for-loop.
    if month in range(1, 8):
        for row in (y_valuesRed_1_2):
            y_MonthIndex = y_valuesRed_1_2[month]
        plt.plot(xData, y_MonthIndex, color = 'red', label = f"Linjediagram för {label[month]}")
#(Gäller jan-aug t.o.m 2021)
#-''-
    elif month in (range(8, 13)):
        for row in (y_valuesRed_1_2):
            y_MonthIndex = y_valuesRed_1_2[month]
            plt.plot(xData[1:], y_MonthIndex, color = 'red', label = f"Linjediagram för {label[month]}")
            break
## resp. medelvärdes-värden med års-värdena inkluderat samt andra finesser, skriver ut diagrammet.
    plt.plot(xData, y_Means21, color = 'black', label = 'Linjediagram för medelkpi')
    plt.bar(xData, y_Means21, color = 'thistle', label = 'kpiMedel')
#Diagrammet med titlar för x och y samt huvudrubrik, x- och y-värden på axlar samt utseende och placering för etikett.
    plt.xlim(1980,2022)
    plt.ylim(100, 400)

    plt.title('Konsumentprisindex År 1980-2021')
    plt.xlabel('År')
    plt.ylabel('Konsumentprisindex')
    plt.grid()
    plt.legend(loc = 'upper left')
    plt.show()
###############- Deluppgift 5 -###############
def scatterDiagram(data_csv): #som inargument är csv-fil som läses in och utifrån det skrivs ett punktdiagram ut.
#Går igenom listan med alla års-värden och tillhörande värden för respektive år.
    for row in data_csv[1:]:
        for element in range(len(row)):
            row[element] = float(row[element])
## Går igenom listan och tar ut resp. års-värden i rad 1 och kolumn 0 samt alla numeriska värden från rad 1 och resterande kolumner (0 ej inräknat.)
    year_Values = [value[0] for value in data_csv[1:]]
    y_ValuesAll = [value[1:] for value in data_csv[1:]]
# Max-värden: anropar tidigare maxValue-funktionen och "plockar" ut index-positionen för respektive max-värde i listan.
    maxValues = []
    maxTuple = maxValue(y_ValuesAll)
    maxValues = [item[1] for item in maxTuple]
# Går igenom och lägger till högsta värdet för resp. år som element i en lista som skrivs ut tillsammans med x-värden när diagrammet senare ritas ut.
    for i in range(len(maxValues)):
        maxValues[i] += 1
## Min-värden: anropar tidigare minValue-funktionen och "plockar" ut index-positionen för respektive min-värde i listan.
    minValues = []
    minTuple = minValue(y_ValuesAll)
    minValues = [item[1] for item in minTuple]
# Går igenom och lägger till minsta värdet för resp. år som element i en lista som skrivs ut tillsammans med x-värden när diagrammet senare ritas ut.
    for i in range(len(minValues)):
        minValues[i] += 1
#Scatter-diagram med två plottade "linjer" med max- resp. min-värden för tillhörande år samt label och vald färg.
    plt.scatter(maxValues, year_Values, color = 'palegreen', label = 'Årsmax')
    plt.scatter(minValues, year_Values, color = 'mediumslateblue', label ='Årsmin')
# -''-
    plt.title('Månad med högsta resp. lägsta årsvärde av KPI under åren 1980-2022')
    plt.ylabel('År')

    plt.xlabel('Månad')
    plt.ylim(1978, 2024)
    plt.xlim(0, 13)
    plt.grid()
    plt.legend(loc = 'lower center')
    plt.show()
###################################### Menyalternativ##########################################

while True: #önskad återupprepande loop med olika val. Använder intergerList för att jämföra rätt lista med integers, inte med strings, då det ger felmeddelande.
    print('\nMeny\n1. Läser in csv-filerna.\n2. Konsumentprisindex under åren 1980– 2022.\n3. Prisutvecklingen för de olika kategorierna 1980 – 2021.\n4. Prisutvecklingen i procentform för de olika kategorierna 1980-2021.\n5. Diagramöver högsta och lägsta årskpi under åren 1980 - 2022.\n6. Avsluta programmet.')
    
    choice = int(input('\nVälj ett menyalternativ (1-6): '))
    
    if choice == 1:
#Läser in följande CSV-filer genom att anropa funktionen och sparar dem till en lista som används i resten av uppgiften för att programmet ska fungera.
        kpi_file1 = input('\nAnge filnamn eller tryck bara på Enter för kpi.csv: ') or 'kpi.csv'
        kpiData = (readFile(kpi_file1))
        kpi_file2 = input('\nAnge filnamn eller tryck bara på Enter för livsmedel.csv: ') or 'livsmedel.csv'
        livsmedelData = (readFile(kpi_file2))
        kpi_file3 = input('\nAnge filnamn eller tryck bara på Enter för tjanster.csv: ') or 'tjanster.csv'
        tjansteData = (readFile(kpi_file3))
    
    elif choice == 2:
#Användaren anger numerisk värde som motsvarar månad, som är ett andra argument till funktionen som anropas samt som första argument är kpiData (från menyval 1).
        month = int(input('Ange vilken månad som ska presenteras (1-12): '))
        print(staphleDiagram(kpiData, month))
    
    elif choice == 3:
#Beroende på input från användaren skrivs ('a', 'b' eller 'c') så anropas funktion med tillhörande argument (från menyval 1) för input.
        input = input('\nVälj att skriva ut antingen den ena eller båda diagrammen av följande alternativ:\na) Livsmedeldata\nb) Tjänstedata\nc) Båda diagrammen.\nSvar: ')
    
        if input == 'a':
            plotta_data(livsmedelData)

        elif input == 'b':
            print(plotta_data(tjansteData))

        elif input == 'c' or 'Båda diagrammen' or 'Båda':
            print(plotta_data(livsmedelData), plotta_data(tjansteData))
    
    elif choice == 4:
#Användaren får ange filnamn alt. trycka på Enter för att anropa funktionen för att automatiskt tillge argument, som skriver ut tabellen.
        choice_list = input('Ange CSV-fil eller tryck på Enter för deafult-mode: ')
        
        if choice_list == 'tjanster.csv':
            MeanAndTotal(tjansteData)
        
        elif choice_list == 'livsmedel.csv':MeanAndTotal(livsmedelData)
    
        if not choice_list:
            MeanAndTotal(livsmedelData), MeanAndTotal(tjansteData) # Eftersom funktionen ej retunerar så printas "None ut i terminalen. För att undvika detta anropas funktionen utan print.
    
    elif choice == 5:
#Om input är 5, anropas grafen med argumentet kpiData.
        scatterDiagram(kpiData)
#Programmet avslutas, en break-sats används för att avsluta while-loopen.
    elif choice == 6:
        print('Tack för denna gång. Programmet avslutas.')
        break
#Felmeddelande om användaren matar in fel värde (gäller dock bara siffor med basen 10, ej float eller strings).

    else:
        print('\nFelaktigt val, försök igen!')
        continue
