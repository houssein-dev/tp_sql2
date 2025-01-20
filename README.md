-- Insérer des données dans la table `deplomes`
INSERT INTO tp2_deplomes (libelle, specialite, etablissement_delivrance, pay)
VALUES
('Diplôme 1', 'Informatique', 'Université 1', 'Pays 1'),
('Diplôme 2', 'Mathématiques', 'Université 2', 'Pays 2'),
('Diplôme 3', 'Physique', 'Université 3', 'Pays 3'),
('Diplôme 4', 'Chimie', 'Université 4', 'Pays 4'),
('Diplôme 5', 'Biologie', 'Université 5', 'Pays 5');

-- Insérer des données dans la table `postes`
INSERT INTO tp2_postes (libelle, description, etablissement)
VALUES
('Poste 1', 'Description 1', 'Établissement 1'),
('Poste 2', 'Description 2', 'Établissement 2'),
('Poste 3', 'Description 3', 'Établissement 3'),
('Poste 4', 'Description 4', 'Établissement 4'),
('Poste 5', 'Description 5', 'Établissement 5');

-- Script pour insérer 10 000 employés dans la table `employes`
DELIMITER $$

CREATE PROCEDURE InsertEmployees()
BEGIN
    DECLARE i INT DEFAULT 1;
    WHILE i <= 10000 DO
        INSERT INTO tp2_employes (matricule, nni, nom, prenom, lieu_naissance, date_naissance, email, salaire, id_diplome, id_post)
        VALUES (
            CONCAT('MATR', i), -- matricule unique
            FLOOR(RAND() * 1000000000), -- nni aléatoire
            CONCAT('Nom', i), -- nom unique
            CONCAT('Prenom', i), -- prénom unique
            CONCAT('Ville', FLOOR(RAND() * 100)), -- lieu de naissance aléatoire
            DATE_ADD('1980-01-01', INTERVAL FLOOR(RAND() * 15000) DAY), -- date de naissance aléatoire
            CONCAT('email', i, '@example.com'), -- email unique
            ROUND(RAND() * 5000 + 15000, 2), -- salaire entre 15 000 et 20 000
            FLOOR(RAND() * 5) + 1, -- id_diplome entre 1 et 5
            FLOOR(RAND() * 5) + 1 -- id_post entre 1 et 5
        );
        SET i = i + 1;
    END WHILE;
END$$

DELIMITER ;

-- Exécuter la procédure
CALL InsertEmployees();

-- Supprimer la procédure après utilisation si nécessaire
DROP PROCEDURE InsertEmployees;
