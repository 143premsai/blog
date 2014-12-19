Comment faire des accord�ons dans des lignes de tableau en Twitter Bootstrap ? Nous verrons que la table pour faire �un tableau n�est pas une si bonne id�e !
Objectif

Faire un tableau dont chaque ligne est cliquable pour afficher un sous-contenu masqu� (partie gauche) et/ou pour naviguer avec des boutons cliquables (partie droite).
images
Il faut donc int�grer le composant collapse de bootstrap  et des boutons styl�s.
Approche 1 avec <table>

Etape 1 : table
Rien � dire, c�est la solution la plus logique, car c�est celle que bootstrap nous propose pour un simple tableau

<tr>
    <td>1</td>
    <td>Mark</td>
    <td>Otto</td>
    <td>@mdo</td>
</tr>
<tr>
    <td>2</td>
    <td>Jacob</td>
    <td>Thornton</td>
    <td>@fat</td>
</tr>
ScreenShot001
Etape 2 : table + collapse
Il faut utiliser la variante sans accordion de la doc bootstrap avec seulement data-target et collapse.
Probl�me : le collapse ne fonctionne pas pour une balise TR en target.
Solution : cr�er un DIV dans un sous-TR (facultatif : ajouter du CSS pour cacher le r�sidu permanent de margin/padding de la ligne cach�e/collapsed) .

<tr class="accordion-toggle"  data-toggle="collapse" data-target="#collapseOne">
    <td>1</td>
    <td>Mark</td>
    <td>Otto</td>
    <td>@mdo</td>
</tr>
<tr>
    <td></td>
    <td colspan="3">
        <div id="collapseOne" class="collapse in">
            Details 1 <br/>
            Details 2 <br/>
            Details 3 <br/>
        </div>
    </td>
</tr>
ScreenShot002
Etape 3 : table + collapse + buttons
Probl�me : un clique sur un bouton provoque un effet de bord d�expand/collapse de la ligne le contenant. C�est g�nant quand on fait nouvel onglet sur un bouton car le d�tails s�affiche.
Solution : il faut emp�cher l�expand/collapse de se d�clencher en cas d�appui sur un bouton. Il faut donc assigner le click expand � chaque cellule td plutot que sur le tr.
�a fonctionne, MAIS le Javascript rame au expand/collapse quand il y a plusieurs dizaines de lignes et sous-lignes sur la page ET il y a du code dupliqu�.

<tr class="accordion-toggle"  >
    <td data-toggle="collapse" data-target="#collapseTwo">1</td>
    <td data-toggle="collapse" data-target="#collapseTwo">Mark</td>
    <td data-toggle="collapse" data-target="#collapseTwo">Otto</td>
    <td data-toggle="collapse" data-target="#collapseTwo">@mdo</td>
    <td><a class="btn btn-primary" href="https://www.google.com/"><i class="icon-search icon-white"></i></a></td>
</tr>
<tr>
    <td></td>
    <td colspan="4">
        <div id="collapseTwo" class="collapse in">
            - Details 1 <br/>
            - Details 2 <br/>
            - Details 3 <br/>
        </div>
    </td>
</tr>
ScreenShot003
Approche 2 avec <div>

Etape 1 : div
On utilise le syst�me de grille sur lequel repose bootstrap.
Probl�me : les styles de table sont perdus.
Solution : (facultatif) Il faut refaire du CSS si l�on veut obtenir le m�me rendu que pr�c�demment (row top border, cell width, header bold).

<div class="row-fluid" >
    <div class="span2">1</div>
    <div class="span2">Mark</div>
    <div class="span2">Otto</div>
    <div class="span2">@mdo</div>
</div>
ScreenShot004
Etape 2 : div + collapse
(idem solution table+collapse)
Probl�me : le curseur ne change pas de forme lors du survole de la ligne cliquable (icone �main�).
Solution : (facultatif) utiliser un style perso ou re-utiliser la class accordion-toggle sur la div collapsable.

<div class="row-fluid" data-toggle="collapse" data-target="#collapseTwo">
    <div class="span1">1</div>
    <div class="span3">Mark</div>
    <div class="span3">Otto</div>
    <div class="span3">@mdo</div>
</div>
<div id="collapseTwo" class="row-fluid collapse in">
    <div class="span1"></div>
    <div class="span9">
        Details 1 <br/>
        Details 2 <br/>
        Details 3 <br/>
    </div>
</div>
ScreenShot005
Etape 3 : div + collapse + buttons
L�ajout de boutons entre �galement en conflit avec le collapse/expand.
Solution : sortir le bouton de la div toggler.

<div class="row-fluid" >
    <div class="accordion-toggle" data-toggle="collapse" data-target="#collapseThree">
        <div class="span1">1</div>
        <div class="span3">Mark</div>
        <div class="span3">Otto</div>
        <div class="span3">@mdo</div>
    </div>
    <div class="span1">
        <button type="button" class="btn btn-primary"><i class="icon-search icon-white"></i></button>
    </div>
</div>
<div id="collapseThree" class="row-fluid collapse in">
    <div class="span1"></div>
    <div class="span9">
        Details 1 <br/>
        Details 2 <br/>
        Details 3 <br/>
    </div>
</div>
ScreenShot006

Conclusion

J�utilise actuellement la version avec DIV apr�s avoir utilis� TABLE. Au final la page n��tait plus assez r�active, le code dupliqu� �tait source de bugs/maintenance et la solution technique avec TABLE n��tait pas toujours compr�hensible, m�me avec la doc de bootstrap � cot�.
COLLAPSABLE TABLE
Pro : style par defaut dans bootstrap, aimer les tables ?
Con : solution de contournement, performances, duplication de code
COLLAPSABLE  DIV
Pro : responsive, performant
Con : styles curseur et tableau � red�finir
