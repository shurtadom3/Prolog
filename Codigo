%Relaciones
uncle(tio_1, persona2).
uncle(tio_2, persona2).
uncle(tio_3, persona2).
child(hijo_1, persona1).
child(hijo_2, persona1).
child(hijo_1, persona2).
child(hijo_1, persona3).
cousin(primo_1, persona1).
cousin(primo_1, persona3).
cousin(primo_2, persona3).
sibling(hermano_1, persona1).
sibling(hermano_1, persona3).
sibling(hermano_2, persona3).
grandparent(abuelo_1, persona2).
grandparent(abuelo_2, persona2).

father(X,Y) :- child(Y,X).
mother(X,Y) :- child(Y,X).

%Calcular_el_nivel_de_consanguinidad
%Nivel_1
nivelConsanguinidad(X,Y,1) :- father(X,Y).
nivelConsanguinidad(X,Y,1) :- mother(X,Y).
nivelConsanguinidad(X,Y,1) :- child(X,Y).

%Nivel_2
nivelConsanguinidad(X,Y,2) :- sibling(X,Y).
nivelConsanguinidad(X,Y,2) :- grandparent(X,Y).

%Nivel_3
nivelConsanguinidad(X,Y,3) :- uncle(X,Y).
nivelConsanguinidad(X,Y,3) :- cousin(X,Y).

%Distribucion_de_herencia
distribuirHerencia(TotalHerencia, NombreFallecido) :-
    findall(X, nivelConsanguinidad(X, NombreFallecido, 1), Nivel1),
    findall(X, nivelConsanguinidad(X, NombreFallecido, 2), Nivel2),
    findall(X, nivelConsanguinidad(X, NombreFallecido, 3), Nivel3),

    length(Nivel1, Conteo1),
    length(Nivel2, Conteo2),
    length(Nivel3, Conteo3),

    PorcentajeTotal is Conteo1 * 30 + Conteo2 * 20 + Conteo3 * 10,

    (PorcentajeTotal > 100 ->
        AjustarValor is 100 / PorcentajeTotal,
        PorcentajeNivel1 is 30 * AjustarValor,
        PorcentajeNivel2 is 20 * AjustarValor,
        PorcentajeNivel3 is 10 * AjustarValor;
        
        PorcentajeRestante is 100 - PorcentajeTotal,
        PorcentajeNivel1 is 30 + (PorcentajeRestante * 30 / PorcentajeTotal),
        PorcentajeNivel2 is 20 + (PorcentajeRestante * 20 / PorcentajeTotal),
        PorcentajeNivel3 is 10 + (PorcentajeRestante * 10 / PorcentajeTotal)),

    distribuir1(Nivel1, TotalHerencia, PorcentajeNivel1),
    distribuir2(Nivel2, TotalHerencia, PorcentajeNivel2),
    distribuir3(Nivel3, TotalHerencia, PorcentajeNivel3).

%Distribuir_herencia_nivel_1
distribuir1([], _, _).
distribuir1([Cabeza | Cola], TotalHerencia, PorcentajeNivel1) :-
    Herencia is TotalHerencia * PorcentajeNivel1 / 100,
    format('Herencia de ~w: ~w~n', [Cabeza, Herencia]),
    distribuir1(Cola, TotalHerencia, PorcentajeNivel1).

%Distribuir_herencia_nivel_2
distribuir2([], _, _).
distribuir2([Cabeza | Cola], TotalHerencia, PorcentajeNivel2) :-
    Herencia is TotalHerencia * PorcentajeNivel2 / 100,
    format('Herencia de ~w: ~w~n', [Cabeza, Herencia]),
    distribuir2(Cola, TotalHerencia, PorcentajeNivel2).

%Distribuir_herencia_nivel_3
distribuir3([], _, _).
distribuir3([Cabeza | Cola], TotalHerencia, PorcentajeNivel3) :-
    Herencia is TotalHerencia * PorcentajeNivel3 / 100,
    format('Herencia de ~w: ~w~n', [Cabeza, Herencia]),
    distribuir3(Cola, TotalHerencia, PorcentajeNivel3).

%Funcion_principal
main :-
    write('Caso 1:'), nl,
    distribuirHerencia(100000, persona1),
    write('Caso 2:'), nl,
    distribuirHerencia(250000, persona2),
    write('Caso 3:'), nl,
    distribuirHerencia(150000, persona3).

:- main.
