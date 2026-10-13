
# Atelier 2 - Stratégies Fetch et Cascade

## Projet AutoLoc

Ce document présente les stratégies de chargement
(FetchType) et de propagation (CascadeType)
utilisées pour les associations JPA du projet AutoLoc.

## Tableau des associations

| Association | Fetch | Cascade | Justification |
|---|---|---|---|
| Contrat - Paiement | LAZY | ALL + orphanRemoval | Un paiement dépend de son contrat. Supprimer le contrat supprime ses paiements. |
| Agence - Vehicule | LAZY | Aucune | Un véhicule peut exister indépendamment de son agence. |
| Agence - Employe | LAZY | Aucune | Les employés ne doivent pas être supprimés automatiquement avec l'agence. |
| Vehicule - Equipement | LAZY | Aucune | Les équipements peuvent être partagés entre plusieurs véhicules. |
| Client - Reservation | LAZY | PERSIST | Enregistrer un client permet d'enregistrer ses nouvelles réservations. |
| Reservation - Vehicule | LAZY | Aucune | Supprimer une réservation ne doit pas supprimer le véhicule. |
| Reservation - Contrat | LAZY | ALL | Les opérations sur une réservation sont propagées à son contrat. |
| Vehicule - Maintenance | LAZY | PERSIST | Enregistrer un véhicule permet d'enregistrer ses nouvelles maintenances. |

## Conclusion

FetchType.LAZY permet d'éviter le chargement
inutile des entités associées.

CascadeType est utilisé uniquement lorsque
la propagation des opérations est nécessaire.

orphanRemoval = true permet de supprimer
automatiquement les paiements retirés
de la collection d'un contrat.
