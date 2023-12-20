-- Creazione della tabella AEREO
CREATE TABLE AEREO (
    TipoAereo VARCHAR(55) PRIMARY KEY,
    NumPasseggeri INT,
    QtaMerci INT
);

-- Creazione della tabella AEROPORTO
CREATE TABLE AEROPORTO (
    Citta VARCHAR(20),
    Nazione VARCHAR(20),
    NumPiste INT,
    PRIMARY KEY (Citta) -- Assumendo che il nome della città sia unico
);
-- Creazione della tabella VOLO
CREATE TABLE VOLO (
    IdVolo CHAR(5) PRIMARY KEY,
    GiornoSett VARCHAR(10),
    CittaPart VARCHAR(20),
    OraPart TIME,
    CittaArr VARCHAR(20),
    OraArr TIME,
    TipoAereo VARCHAR(20),
    NumPasseggeri INT, -- Aggiunta di NumPasseggeri
    FOREIGN KEY (CittaPart) REFERENCES AEROPORTO(Citta),
    FOREIGN KEY (CittaArr) REFERENCES AEROPORTO(Citta),
    FOREIGN KEY (TipoAereo) REFERENCES AEREO(TipoAereo)
);
-- Creazione della tabella PASSEGGERI
CREATE TABLE PASSEGGERI (
    CF CHAR(16) PRIMARY KEY,
    Nome VARCHAR(30),
    Cognome VARCHAR(30),
-- Aggiunto il vincolo per il valore massimo di bagagli
    NumeroBagagli INT CHECK (NumeroBagagli >= 0 AND NumeroBagagli <= 10) 
);


-- Inserimento di dati nella tabella AEREO
INSERT INTO AEREO (TipoAereo, NumPasseggeri, QtaMerci)
VALUES
    ('Airbus A320', 150, 2000),
    ('Boeing 737', 120, 1800),
    ('Airbus A380', 550, 4000),
    ('Boeing 777', 300, 3500),
    ('Boeing 787', 250, 3000);

-- Inserimento di dati nella tabella AEROPORTO
INSERT INTO AEROPORTO (Citta, Nazione, NumPiste)
VALUES
    ('Torino', 'Italia', 2),
    ('Bologna', 'Italia', 3),
    ('Parigi', 'Francia', 4),
    ('Londra', 'Regno Unito', 5),
    ('Sofia', 'Bulgaria', 6);

INSERT INTO VOLO (IdVolo, GiornoSett, CittaPart, OraPart, CittaArr, OraArr, TipoAereo, NumPasseggeri)
VALUES
    ('AZ884', 'Lunedì', 'Torino', '08:00:00', 'Parigi', '10:30:00', 'Airbus A320', 0),
    ('AZ254', 'Martedì', 'Bologna', '12:45:00', 'Londra', '14:30:00', 'Boeing 737', 0),
    ('AZ474', 'Mercoledì', 'Parigi', '18:30:00', 'Sofia', '21:15:00', 'Airbus A380', 0),
    ('AZ274', 'Giovedì', 'Londra', '09:15:00', 'Bologna', '11:00:00', 'Boeing 777', 0),
    ('AZ275', 'Venerdì', 'Sofia', '14:00:00', 'Torino', '16:45:00', 'Boeing 787', 0);

#DOMANDE GENERICHE:
#Quante piste ha Bologna?
SELECT NumPiste
FROM AEROPORTO
WHERE Citta = 'Bologna';

#Le città di provenienza per i voli diretti a Bologna?
SELECT DISTINCT CittaPart
FROM VOLO
WHERE CittaArr = 'Bologna';

#Le città di partenza e arrivo del volo AZ274?
SELECT CittaPart, CittaArr
FROM VOLO
WHERE IdVolo = 'AZ274';
