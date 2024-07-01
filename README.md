# papillon
1. Napraviti crvenu,plavu,zelenu komponentu i spremiti u isti fajl i filtriranu crvenu
% u posebnu .m skriptu smo napravili ovu funkciju, koju cemo kasnije pozivati 

function [boja] = komponenta(slika, RGB) %% naziv mora biti kao komponenta
boja = slika;
vel_u_pikselima = size(slika);
sirina = vel_u_pikselima(1);
visina = vel_u_pikselima(2);

if RGB == 'R'
    for i = 1:1:sirina
        for j = 1:1:visina
            boja(i,j,2) = 0;
            boja(i,j,3) = 0;
        end
    end
end

if RGB == 'G'
    for i = 1:1:sirina
        for j = 1:1:visina
            boja(i,j,1) = 0;
            boja(i,j,3) = 0;
        end
    end
end

if RGB == 'B'
    for i = 1:1:sirina
        for j = 1:1:visina
            boja(i,j,1) = 0;
            boja(i,j,2) = 0;
        end
    end
end


% zatim pravimo drugu .m skriptu u kojoj primjenjujemo filter

% Čitanje slike
slika = imread('macka.jpg');

% Izdvajanje RGB komponenti
crvena = komponenta(slika, 'R');
zelena = komponenta(slika, 'G');
plava = komponenta(slika, 'B');

% Definisanje filtera
h = [1 0 -1; 2 0 -2; 1 0 -1];

% Primjena filtera na cijelu crvenu komponentu slike
filtriranaCrvena = imfilter(crvena, h);

% Prikaz slika
figure(1);
imshow(crvena);
title('Crvena komponenta');

figure(2);
imshow(zelena);
title('Zelena komponenta');

figure(3);
imshow(plava);
title('Plava komponenta');

figure(4);
imshow(filtriranaCrvena);
title('Filtrirana crvena komponenta');

% Čuvanje slika
imwrite(crvena, 'MojaCrvena.jpg');
imwrite(zelena, 'MojaZelena.jpg'); % naziv proizvoljno
imwrite(plava, 'MojaPlava.jpg');
imwrite(filtriranaCrvena, 'MojaFiltriranaCrvena.jpg');


2. ROTIRANJE TROUGLA

close all
clear all
clc
x1=[6 8 7 ]
y1=[3 3 2]
trougao=patch(x1,y1,'r')
x11=x1
y11=y1
axis([3 8 -1 3])
for i=1:30
    x11=x11-0.1
    y11=y11;
    set(trougao,'x',x11,'y',y11)
    pause(3/30)
end

a=x11+1
b=y11-0.5
for i=1:30
    x11=x11+0.1
    y11=y11-0.1;
  set(trougao,'x',x11,'y',y11)
    pause(3/30)
   
end

for i=1:30
         rotate(trougao,[0 0 1],6,[7,-0.5,0])
         pause (0.1)
end

x11=[6 8 7]
y11=[-1 -1 0]
for i=1:30
    x11=x11-0.1
    y11=y11;
    set(trougao,'x',x11,'y',y11)
    pause(2/30)
end
for i=1:30
    x11=x11+0.1
    y11=y11+0.1;
    set(trougao,'x',x11,'y',y11)
    pause(2/30)
end

for i=1:30
      rotate(trougao,[0 0 1],6,[7,2.5,0])
      pause (1/30)
end

 
3. NAJDUZA RIJEC, OBRNE SE, NOVA RECENICA
% Čitanje rečenice
recenica = input('Unesite rečenicu: ', 's');

% Razdvajanje rečenice na reči uz uzimanje u obzir interpunkcijskih znakova
rijeci = regexp(recenica, '\s+', 'split');  % Razdvaja po razmacima, tabulatorima i ostalim prazninama

% Uklanja interpunkcijske znakove s kraja riječi
rijeci = regexprep(rijeci, '[^\w\s]', '');

% Pronalaženje najduže reči
najduza_rijec = '';
for i = 1:numel(rijeci)
    if numel(rijeci{i}) > numel(najduza_rijec)
        najduza_rijec = rijeci{i};
    end
end

% Ispis najduže reči unazad
fprintf('Najduža riječ: %s\n', najduza_rijec);

% Ispis najduže riječi u obrnutom redoslijedu
fprintf('Obrnut redoslijed: %s\n', flip(najduza_rijec));

% Zamena najduže reči u rečenici
nova_recenica = strrep(recenica, najduza_rijec, flip(najduza_rijec));

% Ispis nove rečenice
fprintf('Nova rečenica: %s\n', nova_recenica);



 KAZALJKA NA SATU 2 SEKUNDE

r = 0:0.1:2*pi;
x = sin(r)+5;
y = cos(r)+5;

patch(x,y,'yellow')
x = [5 5 6 6];
y = [4.9 5.1 5.1 4.9];
kazaljka = patch(x,y,'red');

x1 = x;
y1 = y;
smjer = [0 0 1];

pause
for i=1:180
    rotate(kazaljka,smjer,-6)
    pause(1/30)
end



GUI : DVIJE MATRICE, IZ KNJIGE
 
        % Size changed function: UlaznipodaciPanel
        function UlaznipodaciPanelSizeChanged(app, event)
            position = app.UlaznipodaciPanel.Position;
            
        end

% Value changed function: ElementiprvematriceTextArea
        function ElementiprvematriceTextAreaValueChanged(app, event)
            value = app.ElementiprvematriceTextArea.Value;
            
        end

% Button pushed function: IspisirezultateButton
        function IspisirezultateButtonPushed(app, event)
            mat1 = str2num(char(app.ElementiprvematriceTextArea.Value));
            mat2 = str2num(char(app.ElementidrugematriceTextArea.Value));
            %prikaz matrica
            app.PrvamatricaTextArea.Value = mat2str(mat1);
            app.DrugamatricaTextArea.Value = mat2str(mat2);
             % Racunanje i prikaz inverznih matrica
            if det(mat1) ~= 0
                app.InverznamatricaTextArea.Value = mat2str(inv(mat1));
            else
                app.InverznamatricaTextArea.Value = 'N/A';
            end

            if det(mat2) ~= 0
                app.InverznamatricaTextArea_2.Value = mat2str(inv(mat2));
            else
                app.InverznamatricaTextArea_2.Value = 'N/A';
            end
             % Prikaz transponovanih matrica
            app.TransponovanamatricaTextArea.Value = mat2str(mat1');
            app.TransponovanamatricaTextArea_2.Value = mat2str(mat2');
            % Operacije sa matricama
            if isequal(size(mat1), size(mat2))
                app.ZbirmatricaTextArea.Value = mat2str(mat1 + mat2);
                app.RazlikamatricaTextArea.Value = mat2str(mat1 - mat2);
            else
                app.ZbirmatricaTextArea.Value = 'N/A';
                app.RazlikamatricaTextArea.Value = 'N/A';
            end

            if size(mat1, 2) == size(mat2, 1)
                app.ProizvodmatricaTextArea.Value = mat2str(mat1 * mat2);
            else
                app.ProizvodmatricaTextArea.Value = 'N/A';
            end
   

        end
    end

 
GUI: JEDNA MATRICA, DIJAGONALNA,INVERZNA
 
% Button pushed function: DijagonalnaMatricaButton
        function DijagonalnaMatricaButtonPushed(app, event)
    matrixStr = char(app.UnesielementematriceTextArea.Value); % Convert to char
    matrix = str2num(matrixStr); % Convert char to numerical array
    if isempty(matrix)
        app.IspisrezultataTextArea.Value = 'Unesite validnu matricu!';
        return;
    end
    diag_matrix = diag(diag(matrix));
    app.IspisrezultataTextArea.Value = mat2str(diag_matrix);
        end

% Button pushed function: InverznaButton
        function InverznaButtonPushed(app, event)
    matrixStr = char(app.UnesielementematriceTextArea.Value); % Convert to char
    matrix = str2num(matrixStr); % Convert char to numerical array
    if isempty(matrix)
        app.IspisrezultataTextArea.Value = 'Unesite validnu matricu!';
        return;
    end
    if det(matrix) == 0
        app.IspisrezultataTextArea.Value = 'Matrica nema inverznu!';
        return;
    end
    inv_matrix = inv(matrix);
    app.IspisrezultataTextArea.Value = mat2str(inv_matrix);
        end


        % Button pushed function: GornjetrougaonaButton
        function GornjetrougaonaButtonPushed(app, event)
    matrixStr = char(app.UnesielementematriceTextArea.Value); % Convert to char
    matrix = str2num(matrixStr); % Convert char to numerical array
    if isempty(matrix)
        app.IspisrezultataTextArea.Value = 'Unesite validnu matricu!';
        return;
    end
    upper_tri = triu(matrix);
    app.IspisrezultataTextArea.Value = mat2str(upper_tri);

        end

        % Button pushed function: DonjetrougaonaButton
        function DonjetrougaonaButtonPushed(app, event)
    matrixStr = char(app.UnesielementematriceTextArea.Value); % Convert to char
    matrix = str2num(matrixStr); % Convert char to numerical array
    if isempty(matrix)
        app.IspisrezultataTextArea.Value = 'Unesite validnu matricu!';
        return;
    end
    lower_tri = tril(matrix);
    app.IspisrezultataTextArea.Value = mat2str(lower_tri);
        end
    end



 CETIRI PIRAMIDA
clear all
close all

a=3;
h=4;
P=a^2 + 2*a*h;
V=a^2*h./3;

fprintf('Povrsina je:');
disp(P);
fprintf('Zapremina je:');
disp(V);

x = [0 3 3 0];
y = [0 0 3 3];
z = [0 0 0 0];
patch(x,y,z,'y');
grid on;
axis([-2 5 -2 5]);
xlabel('x-osa');
ylabel('y-osa');
zlabel('z-osa');

x = [0 3 1.5];
y = [0 0 1.5];
z = [0 0 4];
patch(x,y,z,'r');
grid on;
axis([-2 5 -2 5]);
xlabel('x-osa');
ylabel('y-osa');
zlabel('z-osa');

x = [0 0 1.5]
y = [0 3 1.5];
z = [0 0 4];
patch(x,y,z,'g');
grid on;
axis([-2 5 -2 5]);
xlabel('x-osa');
ylabel('y-osa');
zlabel('z-osa');

x = [0 3 1.5];
y = [3 3 1.5];
z = [0 0 4];
patch(x,y,z,'b');
grid on;
axis([-2 5 -2 5]);
xlabel('x-osa');
ylabel('y-osa');
zlabel('z-osa');

x = [3 3 1.5];
y = [0 3 1.5];
z = [0 0 4];
patch(x,y,z,'m');
grid on;
axis([-2 5 -2 5]);
xlabel('x-osa');
ylabel('y-osa');
zlabel('z-osa');



SEMAFORIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIII

t = 0:0.1:2*pi;
x_background = [-2 2 2 -2];
y_background = [-8 -8 2 2];

figure;
patch(x_background, y_background, 'k');
axis([-10 10 -10 10]);
hold on;

while true
    % Crvena boja svijetli 50 sekundi
    crveno = patch(sin(t), cos(t), 'red');
    pause(5);  % 50 sekundi

    % Zatim žuta boja svijetli 5 sekundi
    delete(crveno);
    zuto = patch(sin(t), cos(t) - 3, 'yellow');
    pause(2);  % 5 sekundi

    % Zelena boja svijetli 50 sekundi
    delete(zuto);
    zeleno = patch(sin(t), cos(t) - 6, 'green');
    pause(5);  % 50 sekundi



    % Treptanje tri puta po 5 sekundi
    for i = 1:3
        delete(zeleno);
        pause(0.5);  % 0.5 sekundi
        zeleno = patch(sin(t), cos(t) - 6, 'green');
        pause(0.5);  % 0.5 sekundi
    end

    % Nakon treptanja, žuto pa crveno svjetlo
    delete(zeleno);
    zuto = patch(sin(t), cos(t) - 3, 'yellow');
    pause(2);  % 5 sekundi
    delete(zuto);
    crveno = patch(sin(t), cos(t), 'red');
    pause(50);  % 50 sekundi
end

%% ima i ovaj nacin sa manjim semaforom: I OVOOOOOOOOOOOO

% Definisanje kutije semafora
x1 = [-1.2 1.2 1.2 -1.2]; % X koordinate kutije semafora
y1 = [-6.2 -6.2 1.2 1.2]; % Y koordinate kutije semafora
vsemafor = patch(x1, y1, 'black'); % Kreiranje kvadratnog oblika za kutiju semafora i bojanje u crno
hold on % Zadržavanje trenutnog grafa

% Definisanje krugova za svjetla
t = (0:1/360:1)'*2*pi; % Generisanje uglova za kružne oblike
x = sin(t); % X koordinate krugova (sinusna funkcija)
y = cos(t); % Y koordinate krugova (kosinusna funkcija)
crveno = fill(x, y, 'black'); % Kreiranje crvenog svjetla i bojanje u crno
hold on % Zadržavanje trenutnog grafa
zuto = fill(x, y-2.5, 'black'); % Kreiranje žutog svjetla i bojanje u crno (pomjereno za 2.5 dolje)
hold on % Zadržavanje trenutnog grafa
zeleno = fill(x, y-5, 'black'); % Kreiranje zelenog svjetla i bojanje u crno (pomjereno za 5 dolje)
hold on % Zadržavanje trenutnog grafa
axis([-2 5 -7 2]) % Postavljanje granica osi

% Definisanje kutije drugog semafora
x2 = [2.3 4.5 4.5 2.3]; % X koordinate kutije drugog semafora
y2 = [-6.2 -6.2 -2.5 -2.5]; % Y koordinate kutije drugog semafora
msemafor = patch(x2, y2, 'black'); % Kreiranje kvadratnog oblika za kutiju drugog semafora i bojanje u crno
hold on % Zadržavanje trenutnog grafa
x3 = 0.8*cos(t); % X koordinate krugova za drugi semafor (skalirano na 0.8)
y3 = 0.8*sin(t); % Y koordinate krugova za drugi semafor (skalirano na 0.8)
crvenom = fill(x3+3.4, y3-3.4, 'black'); % Kreiranje crvenog svjetla na drugom semaforu i bojanje u crno (pomjereno)
hold on % Zadržavanje trenutnog grafa
zelenom = fill(x3+3.4, y3-5.1, 'black'); % Kreiranje zelenog svjetla na drugom semaforu i bojanje u crno (pomjereno)
hold on % Zadržavanje trenutnog grafa

% Prikaz crvenog svjetla na prvom semaforu
for i = 1:3
    pause(0.5) % Pauza od 0.5 sekundi
    crveno = fill(x, y, 'red'); % Prikaz crvenog svjetla
    hold on % Zadržavanje trenutnog grafa
    zuto = fill(x, y-2.5, 'black'); % Bojanje žutog svjetla u crno
    hold on % Zadržavanje trenutnog grafa
    zeleno = fill(x, y-5, 'black'); % Bojanje zelenog svjetla u crno
    hold on % Zadržavanje trenutnog grafa
end

% Prikaz zelenog svjetla na drugom semaforu
for i = 1:6
    pause(0.5) % Pauza od 0.5 sekundi
    crvenom = fill(x3+3.4, y3-3.4, 'black'); % Bojanje crvenog svjetla na drugom semaforu u crno
    hold on % Zadržavanje trenutnog grafa
    zelenom = fill(x3+3.4, y3-5.1, 'green'); % Prikaz zelenog svjetla na drugom semaforu
    hold on % Zadržavanje trenutnog grafa
end

% Prikaz žutog svjetla na prvom semaforu
for i = 1:3
    pause(0.5) % Pauza od 0.5 sekundi
    crveno = fill(x, y, 'black'); % Bojanje crvenog svjetla u crno
    hold on % Zadržavanje trenutnog grafa
    zuto = fill(x, y-2.5, 'yellow'); % Prikaz žutog svjetla
    hold on % Zadržavanje trenutnog grafa
    zeleno = fill(x, y-5, 'black'); % Bojanje zelenog svjetla u crno
    hold on % Zadržavanje trenutnog grafa
end

% Prikaz crvenog svjetla na drugom semaforu
for i = 1:3
    crvenom = fill(x3+3.4, y3-3.4, 'red'); % Prikaz crvenog svjetla na drugom semaforu
    hold on % Zadržavanje trenutnog grafa
    zelenom = fill(x3+3.4, y3-5.1, 'black'); % Bojanje zelenog svjetla na drugom semaforu u crno
    hold on % Zadržavanje trenutnog grafa
    pause(0.5) % Pauza od 0.5 sekundi
end

% Prikaz zelenog svjetla na prvom semaforu
for i = 1:3
    pause(1) % Pauza od 1 sekunde
    crveno = fill(x, y, 'black'); % Bojanje crvenog svjetla u crno
    hold on % Zadržavanje trenutnog grafa
    zuto = fill(x, y-2.5, 'black'); % Bojanje žutog svjetla u crno
    hold on % Zadržavanje trenutnog grafa
    zeleno = fill(x, y-5, 'green'); % Prikaz zelenog svjetla
    hold on % Zadržavanje trenutnog grafa
end

% Titranje zelenog svjetla na prvom semaforu
for i = 1:3
    pause(0.5) % Pauza od 0.5 sekundi
    crveno = fill(x, y, 'black'); % Bojanje crvenog svjetla u crno
    hold on % Zadržavanje trenutnog grafa
    zuto = fill(x, y-2.5, 'black'); % Bojanje žutog svjetla u crno
    hold on % Zadržavanje trenutnog grafa
    zeleno = fill(x, y-5, 'black'); % Bojanje zelenog svjetla u crno
    hold on % Zadržavanje trenutnog grafa
    pause(0.5) % Pauza od 0.5 sekundi
    zeleno = fill(x, y-5, 'green'); % Prikaz zelenog svjetla
    hold on % Zadržavanje trenutnog grafa
end

% Promjena zelenog svjetla na prvom semaforu u žuto
pause(0.5) % Pauza od 0.5 sekundi
zeleno = fill(x, y-5, 'black'); % Bojanje zelenog svjetla u crno
hold on % Zadržavanje trenutnog grafa
zuto = fill(x, y-2.5, 'yellow'); % Prikaz žutog svjetla
hold on % Zadržavanje trenutnog grafa
pause(2) % Pauza od 2 sekunde

% Promjena žutog svjetla na prvom semaforu u crveno
zuto = fill(x, y-2.5, 'black'); % Bojanje žutog svjetla u crno
hold on % Zadržavanje trenutnog grafa
crveno = fill(x, y, 'red'); % Prikaz crvenog svjetla
hold on % Zadržavanje trenutnog grafa

% Promjena drugog semafora na zeleno svjetlo
crvenom = fill(x3+3.4, y3-3.4, 'black'); % Bojanje crvenog svjetla na drugom semaforu u crno
hold on % Zadržavanje trenutnog grafa
zelenom = fill(x3+3.4, y3-5.1, 'green'); % Prikaz zelenog svjetla na drugom semaforu
hold on % Zadržavanje trenutnog grafa


LENIJAR KAZALJKA

 
x=[-1 7 7 -1];
y=[0 0 -7 -7]
bg=patch(x,y,'w')
hold on
xl = [0 6 6 0];
yl = [-1 -1 -2 -2];
linijar = patch(xl, yl, 'w');
hold on

text(0.15,-1.75,'0')
text(0.25,-2,'|')
text(0.75,-2,'|')
text(1.25,-2,'|')
text(1.75,-2,'|')
text(2.25,-2,'|')
text(2.75,-2,'|')
text(3.25,-2,'|')
text(3.75,-2,'|')
text(4.25,-2,'|')
text(4.75,-2,'|')
text(5.25,-2,'|')
text(5.75,-2,'|')
text(5.7,-1.75,'12')
hold all

xk=[0.2 0.2 0 0.25 0.5 0.3 0.3];
yk=[-4 -2.2 -2.2 -2 -2.2 -2.2 -4];
strelicaa=patch(xk,yk,'r')

for i=1:11
    
    xk=xk+0.5;
    yk=yk;
    pause(1/11)
    set(strelicaa,'x',xk,'y',yk)
end
for i=1:11
   
    xk=xk-0.5;
    yk=yk;
    pause(2/11)
    set(strelicaa,'x',xk,'y',yk,'facecolor','blue');
end

PETOUGAO SE OKRECE PREMA GORE
 
clear all
close all
clc

figure
t=(1/10:1/5:1)'*2*pi;
x=sin(t);
y=cos(t);
axis([-2 12 -2 8])
h=patch(x,y,'r');
xlabel('x'); 
ylabel('y'); 
zlabel('z');
title('Rotacija i translacija petougla');
grid ON
pause(2)

x1=x;
y1=y;

x2=0;
y2=0;

for t=1:1:60
    x1=x1+(1/6);
    y1=y1+(0.1);
    x2=x2+(1/6);
    y2=y2+(0.1);
    
    set(h,'x',x1,'y',y1)
    rotate(h, [0 0 1], t*30, [x2 y2 0])
    
    pause(0.03)
end




SNI SLOGOVI
% Unos teksta sa tastature
tekst = input('Unesite tekst: ', 's');

% Prebrojavanje i indeksi slogova 'sni'
indeksi_sni = strfind(tekst, 'sni');
broj_sni = length(indeksi_sni);

fprintf('Broj pojavljivanja sloga ''sni'': %d\n', broj_sni);
if broj_sni > 0
    fprintf('Indeksi pojavljivanja sloga ''sni'': %s\n', mat2str(indeksi_sni));
end

% Brojanje praznih mjesta (razmaka)
indeksi_razmaka = find(isspace(tekst));
broj_razmaka = length(indeksi_razmaka);

fprintf('Broj praznih mjesta (razmaka): %d\n', broj_razmaka);
if broj_razmaka > 0
    fprintf('Indeksi praznih mjesta: %s\n', mat2str(indeksi_razmaka));
end

% Brojanje rečenica
recenice = strsplit(tekst, {'.' '!' '?'});
broj_recenica = length(recenice);

% Brojanje vrsta rečenica
broj_upitnih = sum(endsWith(recenice, '?'));
broj_uzvicnih = sum(endsWith(recenice, '!'));
broj_izjavnih = broj_recenica - broj_upitnih - broj_uzvicnih;

fprintf('Broj rečenica: %d\n', broj_recenica);
fprintf('Broj upitnih rečenica: %d\n', broj_upitnih);
fprintf('Broj uzvičnih rečenica: %d\n', broj_uzvicnih);
fprintf('Broj izjavnih rečenica: %d\n', broj_izjavnih);

% Brojanje riječi
rijeci = strsplit(tekst);
broj_rijeci = length(rijeci);

fprintf('Broj riječi: %d\n', broj_rijeci);

 FILTERI RAZLICITI
% Učitavanje originalne slike
originalna_slika = imread('macka.jpg');

% Filtriranje slika s različitim filterima
sobel_slika = imfilter(originalna_slika, fspecial('sobel'));
motion_slika = imfilter(originalna_slika, fspecial('motion', 15, 45));
log_slika = imfilter(originalna_slika, fspecial('log', 5, 0.5));
disk_slika = imfilter(originalna_slika, fspecial('disk', 5));
unsharp_slika = imfilter(originalna_slika, fspecial('unsharp'));

% Prikaz originalne slike i filtriranih slika
figure;

subplot(2, 3, 1);
imshow(originalna_slika);
title('Originalna slika');

subplot(2, 3, 2);
imshow(sobel_slika);
title('Sobel filter');

subplot(2, 3, 3);
imshow(motion_slika);
title('Motion filter');

subplot(2, 3, 4);
imshow(log_slika);
title('Log filter');

subplot(2, 3, 5);
imshow(disk_slika);
title('Disk filter');

subplot(2, 3, 6);
imshow(unsharp_slika);
title('Unsharp filter');

%% Iz knjige: ISTI ZADATAK

s=imread('buket.jpg');
I=im2double(s);
subplot(3,2,1),imshow(I), title('Original');

H=fspecial('motion',30,60);
Motion=imfilter(I,H,'replicate');
subplot(3,2,2),imshow(Motion),title('Motion');


H=fspecial('sobel');
Sobel=imfilter(I,H,'replicate');
subplot(3,2,3),imshow(Sobel),title('Sobel');

H=fspecial('log',[30,100],0.2);
Log=imfilter(I,H,'replicate');
subplot(3,2,4),imshow(Log),title('Log');

H=fspecial('disk',20);
Disk=imfilter(I,H,'replicate');
subplot(3,2,5),imshow(Disk),title('Disk');

H=fspecial('unsharp');
Unsharp=imfilter(I,H,'replicate');
subplot(3,2,6),imshow(Unsharp),title('Unsharp');

 SUNCEEEEEEEEEEE 5 PUTA U 2 SEKUNDE
clc
clearvars

% Parametri
r_kruga = 1.4; % Radijus kruga
broj_trokuta = 8; % Broj trokuta
broj_rotacija = 5; % Broj rotacija
vrijeme_animacije = 2; % Ukupno vrijeme animacije (sekunde)
broj_koraka = 240; % Broj koraka animacije

% Definiranje kruga
t = linspace(0, 2*pi, 100);
x_krug = r_kruga * sin(t);
y_krug = r_kruga * cos(t);
% Definiranje trokuta
x_trokut = [1.5 2.5 1.5];
y_trokut = [-0.5 0 0.5];

% Stvaranje grafičkog prozora
figure;
axis([-3 3 -3 3]);
grid on;
hold on;

% Crteži
patch(x_krug, y_krug, 'yellow');

% Inicijalizacija niza za trokute i rotacija
trokut = gobjects(1, broj_trokuta);
deg = 360 / broj_trokuta;

for i = 1:broj_trokuta
    trokut(i) = patch(x_trokut, y_trokut, 'yellow');
    rotate(trokut(i), [0 0 1], deg * (i - 1));
end

% Računanje koraka rotacije
koraci_rotacije = linspace(0, 360 * broj_rotacija, broj_koraka);
% Animacija rotacije
for i = 1:broj_koraka
    for j = 1:broj_trokuta
        rotate(trokut(j), [0 0 1], koraci_rotacije(i) / broj_koraka);
    end
    pause(vrijeme_animacije / broj_koraka);
end


 GUI : RECENICE
% Button pushed function: StartButton
        function StartButtonPushed(app, event)
              % Get input text
            text = app.InputTextArea.Value;
            text = string(text);
            % Count words
            
            words = strsplit(text);
            numWords = length(words);

            
            % Count exclamation sentences
            numExclSentences = numel(strfind(text, '!'));
            numPeriodSentences = numel(strfind(text, '.'));
            numQuestionSentences = numel(strfind(text, '?'));
            numSentences = numExclSentences + numPeriodSentences + numQuestionSentences;
            % Count vowels
            textlower = lower(text);
            numa = numel(strfind(textlower, 'a'));
            nume = numel(strfind(textlower, 'e'));
            numi = numel(strfind(textlower, 'i'));
            numo = numel(strfind(textlower, 'o'));
            numu = numel(strfind(textlower, 'u'));

            numVowels = numa+nume+numi+numo+numu;



            % Count non-vowels
            numNonVowels = sum(isletter(text)) - numVowels;  % Count all letters minus vowels

            % Update fields
            app.WordsEditField.Value = num2str(numWords);
            app.SentencesEditField.Value = num2str(numSentences);
            app.ExclSentencesEditField.Value = num2str(numExclSentences);
            app.PeriodSentencesEditField.Value = num2str(numPeriodSentences);
            app.QuestionSentencesEditField.Value = num2str(numQuestionSentences);
            app.VowelsEditField.Value = num2str(numVowels);
            app.NonVowelsEditField.Value = num2str(numNonVowels);


        end

        % Button pushed function: DeleteButton
        function DeleteButtonPushed(app, event)
            app.InputTextArea.Value = '';
            
            % Clear the results fields
            app.WordsEditField.Value = num2str(0);
            app.SentencesEditField.Value = num2str(0);
            app.ExclSentencesEditField.Value =num2str(0);
            app.PeriodSentencesEditField.Value =num2str(0);
            app.QuestionSentencesEditField.Value = num2str(0);
            app.VowelsEditField.Value = num2str(0);
            app.NonVowelsEditField.Value = num2str(0);
      
        end
    end



 
GUI: SPAJANJE RIJECI, KOLIKOVA SLOVA....
 
% Button pushed function: SpajanjeRijeciButton
        function SpajanjeRijeciButtonPushed(app, event)
        % Uzmi tekst iz EditField
        sentence = app.EditField.Value;
        
        % Razdvoji riječi po razmacima (ili drugim separatorima ako su uneseni)
        words = strsplit(sentence);  % Razdvaja riječi po razmacima
       
        mergedSentence = strjoin(words, '');  % Spaja riječi razmakom
        
        % Postavi spojeni tekst u ResultTextArea
        app.ResultTextArea.Value = mergedSentence;
        end

        % Button pushed function: SlovaiSuglasniciButton
        function SlovaiSuglasniciButtonPushed(app, event)
            sentence = app.EditField.Value;
            vowels = 'aeiouAEIOU';
            numVowels = sum(ismember(sentence, vowels));
            numNonVowels = sum(~ismember(sentence, vowels) & isletter(sentence));
            app.ResultTextArea.Value = sprintf('Broj slova: %d\nBroj suglasnika: %d\n', numVowels + numNonVowels, numNonVowels);
        end

        % Button pushed function: 
        % BrojRecenicaBrojRijeciBrojSuglasnikaButton
        function BrojRecenicaBrojRijeciBrojSuglasnikaButtonPushed(app, event)
            sentence = app.EditField.Value;
            words = strsplit(sentence);
            result = '';
            vowels = 'aeiouAEIOU';
            
            for i = 1:length(words)
                word = words{i};
                numVowels = sum(ismember(word, vowels));
                result = [result, sprintf('Riječ: %s\n Broj slova: %d\n Broj samoglasnika: %d\n Samoglasnici: %s\n', ...
                    word, length(word), numVowels, word(ismember(word, vowels)))];
            end
            
            app.ResultTextArea.Value = result;
        end
    end


 SESTOUGAO LIJEVO DESNO PO PRAVOUOGANIKU
clc 
clear all 
close all 

x=[0 10 10 0]; % X-koordinate pravougaonika ili oblika
y=[0 0 0.8 0.8]; % Y-koordinate pravougaonika ili oblika
patch(x,y,'r'); % Kreira popunjenu poligon (pravougaonik) crvene boje
hold on; % Zadržava trenutni graf i određene svojstva

t=(1/12:1/6:1)'*2*pi; % Generiše uglove od 0 do 2*pi radijana
x1=sin(t)+1; % X-koordinate kruga na osnovu sinusa uglova, pomaknuto za 1
y1=cos(t)+2; % Y-koordinate kruga na osnovu kosinusa uglova, pomaknuto za 2
h=fill(x1,y1,'y'); % Kreira popunjeni žuti krug koristeći izračunate koordinate

axis([-2 12 -12 12]); % Postavlja granice osa za prikaz od -2 do 12 po x-osi i -12 do 12 po y-osi
grid on; % Uključuje prikaz mreže na grafikonu

x11=x1; % Postavlja početne X-koordinate za rotaciju
y22=y1; % Postavlja početne Y-koordinate za rotaciju
cx=1;   % Početna X-koordinata centra rotacije

for k=1:5
    for i=1:30
        zdir=[0 0 1];   % Z-os rotacije (ovdje znači rotacija oko Z-os)
        center=[cx 2 0]; % Koordinate centra rotacije
        
        set(h,'x',x11,'y',y22); % Postavlja nove X i Y koordinate kruga
        rotate(h,zdir,i*30,center); % Vrši rotaciju kruga za i*30 stepeni oko centra
        
        cx=cx+0.27444;  % Pomiče X koordinatu centra rotacije
        x11=x11+0.27444; % Pomiče X koordinate kruga
        y22=y22;        % Y koordinate kruga ostaju iste
        
        pause(0.025);   % Pauzira izvršavanje koda na 0.025 sekundi
    end
    
    for j=1:30
        zdir=[0 0 1];   % Z-os rotacije (ovdje znači rotacija oko Z-os)
        cx=cx;          % X koordinata centra rotacije ostaje ista
        center=[cx 2 0]; % Koordinate centra rotacije
        
        set(h,'x',x11,'y',y22); % Postavlja nove X i Y koordinate kruga
        rotate(h,zdir,j*30,center); % Vrši rotaciju kruga za j*30 stepeni oko centra
        
        x11=x11-0.27444; % Pomiče X koordinate kruga unazad
        y22=y22;         % Y koordinate kruga ostaju iste
        cx=cx-0.27444;   % Pomiče X koordinatu centra rotacije unazad
        
        pause(0.025);    % Pauzira izvršavanje koda na 0.025 sekundi
    end
end

%% SA DRAJVAAA ISTI ZADATAK

clc
clear all
close all
x=[0 10 10 0]
y=[0 0 0.8 0.8]
patch(x,y,'r')
hold on

t=(1/12:1/6:1)'*2*pi
x1=sin(t)+1
y1=cos(t)+2
h=fill(x1,y1,'y');
axis([-2 12 -12 12])
grid on
x11=x1;
y22=y1;
cx=1;

for k=1:5
for i=1:30
zdir=[0 0 1];
center=[cx 2 0]    

    set(h,'x',x11,'y',y22)
    rotate(h,zdir,i*30,center)
    cx=cx+0.27444;
  
    x11=x11+0.27444;
    y22=y22;
    
    pause(0.025)
end

for j=1:30
    zdir=[0 0 1];
     cx=cx;
     center=[cx 2 0];
  
    set(h,'x',x11,'y',y22)
    rotate(h,zdir,j*30,center) 
      x11=x11-0.27444;
    y22=y22;
    cx=cx-0.27444;
    pause(0.025)
end
end


 
NISKOPROPUSNI FILTER, WS,WP..
clear all
clc

fs=44000;
Wp=[2*1000/fs];
Ws=[2*1300/fs]; 
Rp=1;
Rs=40;

d=fdesign.lowpass('Fst,Fp,Ast,Ap',Ws,Wp,Rs,Rp);
f=design(d,'cheby2');
info(f)
fvtool(f)
[Y,FS]=wavread('matlab.wav');
t=0:1/fs:1/fs*(length(Y)-1);
plot(t,Y)
xlabel('Vrijeme [s]')
ylabel('Amplituda')
hold on
izlaz=filter(f,Y);
plot(t,izlaz,'r-')
legend('Ulazni signal','Filtrirani signal')



GUI: FUNKCIJA KOJA IMA OMEGU I FI
% Button pushed function: PrikaziButton
        function PrikaziButtonPushed(app, event)
            % Get parameter values from GUI
            T = app.TEditField.Value;
            omega = app.OmegaEditField.Value;
            phi = app.PhiEditField.Value;
            t_min = app.TminEditField.Value;
            t_max = app.TmaxEditField.Value;

            % Generate time vector
            t = linspace(t_min, t_max, 100);

            % Calculate function f(t)
            f = exp(-t/T) .* sin(omega*t + phi);

            % Plot the function
            plot(app.UIAxes, t, f);
            xlabel(app.UIAxes, 't');
            ylabel(app.UIAxes, 'f(t)');
            title(app.UIAxes, 'Prikaz funkcije');
        end
    end




GUI: SMAJLIC SRETNI TURZNI

% Button pushed function: SretniButton
        function SretniButtonPushed(app, event)
% Kreiranje koordinata za smajlića
    t = 0:pi/50:2*pi;
    x_head = 4 * cos(t);
    y_head = 4 * sin(t);
    
    x_eye1 = cos(t) - 2;
    y_eye1 = sin(t) + 1.5;
    
    x_eye2 = cos(t) + 2;
    y_eye2 = sin(t) + 1.5;
    
    t_mouth = pi:pi/50:2*pi;
    x_mouth = 3 * cos(t_mouth);
    y_mouth = 3 * sin(t_mouth);
    
        % Prikazivanje smajlića na UIAxes komponenti
    plot(app.UIAxes, x_head, y_head, 'LineWidth', 2, 'Color', 'yellow');
    hold(app.UIAxes, 'on');  % Drži trenutni grafikon
    
    plot(app.UIAxes, x_eye1, y_eye1, 'LineWidth', 2, 'Color', 'black');
    plot(app.UIAxes, x_eye2, y_eye2, 'LineWidth', 2, 'Color', 'black');
    plot(app.UIAxes, x_mouth, y_mouth, 'LineWidth', 2, 'Color', 'black');
    
    hold(app.UIAxes, 'off');  % Završi držanje grafikona

        end

        % Button pushed function: TuzniButton
        function TuzniButtonPushed(app, event)
% Kreiranje koordinata za tužnog smajlića
t = 0:pi/50:2*pi;
    x = 4 * cos(t);
    y = 4 * sin(t);
    
    t1 = 0:pi/50:2*pi;
    x1 = cos(t1) - 2;
    y1 = sin(t1) + 1.5;
    
    t2 = 0:pi/50:2*pi;
    x2 = cos(t2) + 2;
    y2 = sin(t2) + 1.5;
    
    t3 = pi:pi/50:2*pi;
    x3 = 3 * cos(t3);
    y3 = -3 * sin(t3) - 2.3;
    
       % Prikazivanje tužnog smajlića na UIAxes komponenti
    plot(app.UIAxes, x, y, 'LineWidth', 2, 'Color', 'yellow');
    hold(app.UIAxes, 'on');  % Drži trenutni grafikon
    
    plot(app.UIAxes, x1, y1, 'LineWidth', 2, 'Color', 'black');
    plot(app.UIAxes, x2, y2, 'LineWidth', 2, 'Color', 'black');
    plot(app.UIAxes, x3, y3, 'LineWidth', 2, 'Color', 'black');
    
    hold(app.UIAxes, 'off');  % Završi držanje grafikona
        end
    end


 KUGLA KOJA SE KRECE LIJEVO DESNO 3 SEKUNDE
x1=0;
y1=-0.5:0.001:0.1;
x2=4;
y2=-0.5:0.001:0;
y3=0;
x3=0:0.01:4;
plot(x1*ones(size(y1)), y1, x2*ones(size(y2)), y2, x3, y3*ones(size(x3)), 'LineWidth', 4)
hold on
t=(0:1/720:1)'*2*pi;
x=0.1+0.1*sin(t);
y=0.1+0.1*cos(t);
h=fill(x,y,'b')
axis([-0.5 4.5 -0.5 2])
xr=x;
yr=y;
a=0;b=0;c=0;
for i=1:80
    xr=xr+(3.8/80);
    a=a+(3.8/80);
    yr=yr;
    pause(3/80)
    set(h,'x',xr,'y',yr)
    rotate(h,[0 0 1],10,[a b 0])
end
for i=1:80
    xr=xr-(3.8/80);
    a=a-(3.8/80);
    yr=yr;
    pause(3/80)
    set(h,'x',xr,'y',yr)
    rotate(h,[0 0 1],10,[a b 0])
end






GUI: ZASTAVA

% Button pushed function: PromijeniBojuButton
        function PromijeniBojuButtonPushed(app, event)
% Clear previous plot
    cla(app.UIAxes);

    % Generate random color for the flag
    color = rand(1, 3); % Random RGB color

    % Generate data
    t = 0:0.1:4*pi;
    y1 = 1/2*sin(t) - 1;
    y2 = 1/2*sin(t) + 1;

    % Plot on UIAxes
    hold(app.UIAxes, 'on');
    area(app.UIAxes, t, y2, 'FaceColor', color, 'EdgeColor', color);
    area(app.UIAxes, t, y1, 'FaceColor', color, 'EdgeColor', color);
    hold(app.UIAxes, 'off');

    % Set axes properties
    xlabel(app.UIAxes, 'X osa');
    ylabel(app.UIAxes, 'Y osa');
    title(app.UIAxes, 'Grafikon na UI Axes');
    axis(app.UIAxes, [-2 15 -2 2]); % Set axis limits
        end
    end

 
ANIMACIJA TACKE KROZ PUTANJU 5COST,2SINT,T
% 1. zadatak 
clear all
clc
close all

% generiranje objekta
t = linspace(0,2*pi,100);
x = 5*cos(t);
y = 2*sin(t);
z = t;

% iscrtavanje
figure

clf % clear figure
for k = 1:length(t)
    %estraktovati podatke trenutne pozicije za svaki frame
    t_k = t(k);
    x_t = x(k);
    y_t = y(k);
    z_t = z(k);
    
    % iscrtavanje trenutne lokacije
    plot3(x_t,y_t,z_t,'go','Linewidth',3,'MarkerSize',15);
    
    % iscrtavanje cijele putanje
    hold on
    plot3(x,y,z,'b-','LineWidth',2);
    grid on
    xlabel('x-osa');
    ylabel('y-osa');
    zlabel('z-osa');
    title(['Tacka je na putanji t=', num2str(t_k),' sekundi']);
    view([30 35]);
    movieVector(k) = getframe; % ili drawnow, ili da sacuvamo brzinu iscrtavanja pause(0.2)
    %Sacuvaj movie
    myWriter = VideoWriter('krivulja','MPEG-4');
    myWriter.FrameRate = 20;
    
    %otvori i pokreni spremljeni movie
    open(myWriter);
   
    writeVideo(myWriter);
end


 RIJEC POCINJE SA I ZAVRSAVA SA D
clc;
clear;

% Inicijalizacija varijabli
words = {}; % Lista za spremanje unesenih riječi
vowels = 'aeiou'; % Samoglasnici
finalWord = ''; % Posljednja riječ koja zadovoljava uvjet
count = 0; % Brojač unesenih riječi

while true
    % Unos riječi s tastature
    word = input('Unesite riječ: ', 's');
    words{end + 1} = word;
    count = count + 1;
    
    % Provjera da li riječ zadovoljava uvjet
    if startsWith(word, 'i') && endsWith(word, 'd')
        % Provjera da li riječ sadrži samo samoglasnike (osim prvog i posljednjeg slova)
        middle = word(2:end-1);
        if all(ismember(middle, vowels))
            finalWord = upper(word);
            words{end} = finalWord; % Zamjena originalne riječi sa riječi u velikim slovima
            break;
        end
    end
end

% Pretvaranje svih riječi u niz s velikim samoglasnicima, osim zadnje riječi
for i = 1:length(words) - 1
    word = words{i};
    for j = 1:length(word)
        if ismember(word(j), vowels)
            word(j) = upper(word(j));
        end
    end
    words{i} = word;
end

% Ispis rezultata
fprintf('Ukupan broj unesenih riječi: %d\n', count);
fprintf('Sve unijete riječi sa velikim samoglasnicima:\n');
disp(words);

 
 

 ANIMACIJA TACKE 8COST,5SINT,2T
 
clear all
clc
close all

% generiranje objekta
t = linspace(0,2*pi,100);
x = 8*cos(t);
y = 5*sin(t);
z = 2*t;

% iscrtavanje
figure

clf % clear figure
for k = 1:length(t)
    %estraktovati podatke trenutne pozicije za svaki frame
    t_k = t(k);
    x_t = x(k);
    y_t = y(k);
    z_t = z(k);
    
    % iscrtavanje trenutne lokacije
    plot3(x_t,y_t,z_t,'go','Linewidth',3,'MarkerSize',15);
    
    % iscrtavanje cijele putanje
    hold on
    plot3(x,y,z,'b-','LineWidth',2);
    grid on
    xlabel('x-osa');
    ylabel('y-osa');
    zlabel('z-osa');
    title(['Tacka je na putanji t=', num2str(t_k),' sekundi']);
    view([30 35]);
    movieVector(k) = getframe; % ili drawnow, ili da sacuvamo brzinu iscrtavanja pause(0.2)
    %Sacuvaj movie
    myWriter = VideoWriter('krivulja','MPEG-4');
    myWriter.FrameRate = 20;
    
    %otvori i pokreni spremljeni movie
    open(myWriter);
   
    writeVideo(myWriter);
end


 GUI : MATRICA A U B 
       % Button pushed function: IzracunajButton
        function IzracunajButtonPushed(app, event)
            A_str = app.ElementiMatriceATextArea.Value;

% Split the input string into lines
lines = splitlines(A_str);

% Initialize matrix A
A = [];

% Iterate through each line and convert to numbers
for i = 1:numel(lines)
    line = strtrim(lines{i}); % Remove leading/trailing whitespace
    if ~isempty(line)
        row = str2double(strsplit(line)); % Convert line to numbers
        A = [A; row]; % Append row to matrix A
    end
end

% Check if A is empty or not a valid matrix
if isempty(A) || any(isnan(A(:)))
    % Display error if input is not a valid matrix
    app.OutputTextArea.Value = 'Error: Invalid matrix input.';
    return;
end


    % Calculate matrix B
    % a) Exclude the last column of A
    B_a = A(:, 1:end-1);

    % b) Exclude the first row of A
    B_b = A(2:end, :);

    % c) Change signs of elements in the intersection of last row and first column
    A(end, 1) = -A(end, 1);
    B_c = A;

    % Display matrix B in OutputTextArea
    app.ElementiMatriceBTextArea.Value = sprintf(['B (iskljucenje zadnje kolone):\n%s\n\nB (iskljucenje prvog reda):\n%s\n\nB (presjek' ...
        '):\n%s'], ...
        mat2str(B_a), mat2str(B_b), mat2str(B_c));
        end
    end


 
 LINEARNO POJACANJE ZVUKA I INVERZIJA
clc 
clear all 
close all

[zvuk,fs] = audioread('sound.mp3'); 
ramp = 0:1/(length(zvuk)-1):1; 
linearno_pojacanje = zvuk.*ramp'; 
inverzija = zvuk .* (1 - ramp');
t = 0:1/fs:1/fs*(length(zvuk)-1); 
subplot(211)
plot(t,zvuk)
title('Ulazni zvucni signal'); 
axis([0 2 -1 1])
subplot(212)
plot(t,linearno_pojacanje)
hold on 
plot(t, inverzija, 'g', 'LineWidth', 2);
plot(t, ramp, 'r', 'LineWidth', 2);
title('Linearno pojacanje i inverzija signala');
xlabel('Vrijeme (s)');
ylabel('Amplituda');
legend('Linearno pojacanje', 'Inverzija', 'Ramp', 'Location', 'best');
axis([0 2 -1 1]);
 


 VISOKOPROPUSNI FILTER SA A I B
% 1. a)
Fs=4000;
T=1/Fs;
L=1000;
t=(0:L-1)*T;

y=0.7*sin(2*pi*300*t)+sin(2*pi*700*t);
subplot(211)
plot(t(1:200),y(1:200))
title('Sinusni signal');
xlabel('Vrijeme');
ylabel('Amplituda');

NFFT=2^nextpow2(L);
Y=fft(y,NFFT)/L;
f=Fs/2*linspace(0,1,NFFT/2+1);
subplot(212)
plot(f,2*abs(Y(1:NFFT/2+1)),'r')
xlabel('Frekvencija');
ylabel('Funkcija y');

%% b)
clear all
clc

fs=44000;
Wp=[2*3000/fs];
Ws=[2*2900/fs];
Rp=1;
Rs=40;

d=fdesign.highpass('Fst,Fp,Ast,Ap',Ws,Wp,Rs,Rp);
f=design(d,'cheby2');
info(f)
fvtool(f)
[Y,FS]=wavread('matlab.wav');
t=0:1/fs:1/fs*(length(Y)-1);
plot(t,Y)
xlabel('Vrijeme [s]')
ylabel('Amplituda')
hold on
izlaz=filter(f,Y);
plot(t,izlaz,'r-')
legend('Ulazni signal','Filtrirani signal')






%%  KENINO 

%a)
s=sin([1:4000*1]*2*pi*300/4000);
s2=sin([1:4000*1]*2*pi*700/4000);
t=linspace(0,1,length(s));
t1=linspace(0,1,length(s2));
subplot(411)
plot(t,s)
xlabel('Vrijeme s');
ylabel('Amplituda');
title('Generisani cisti ton')

subplot(412)
plot(t(1:200),s(1:200))
xlabel('Vrijeme')
ylabel('Amplituda');
title('Vremenski uzorak cistog tona')

subplot(413)
plot(t1,s2)
xlabel('Vrijeme s');
ylabel('Amplituda');
title('Generisani cisti ton')

subplot(414)
plot(t1(1:200),s2(1:200))
xlabel('Vrijeme')
ylabel('Amplituda');
title('Vremenski uzorak cistog tona')

%%
%b)
fs=44000;
Wp=[2*3000/fs];
Ws=[2*2900/fs];
Rp=1;
Rs=40;
d=fdesign.highpass('Fst,Fp,Ast,Ap',Ws,Wp,Rs,Rp);
f=design(d,'cheby2');
info(f)
fvtool(f)


 VENTILATOR
figure
theta=0:pi/100:2*pi;
rho=sin(theta*3);
subplot(2,1,1),h=polar(theta,rho,'go');
pause
for i=1:60
    zdir=[0 0 1];
    center=[0 0 0];
    pause(2/60)
    rotate(h,zdir,6,center)
end
pause
[x,y]=meshgrid([-2:0.1:2]);
z=sin(x.^2+y.^2);
subplot(2,1,2),h=surf(x,y,z)
pause
axis tight
for i=1:100
    zdir=[0 0 -1];
    center=[0 0 0];
    rotate(h,zdir,7.2,center)
    pause(5/100)
end





 SLIKA U ZASEBNE FOLDERE

function [boja] = komponenta(slika, RGB) %% naziv mora biti kao komponenta
boja = slika;
vel_u_pikselima = size(slika);
sirina = vel_u_pikselima(1);
visina = vel_u_pikselima(2);

if RGB == 'R'
    for i = 1:1:sirina
        for j = 1:1:visina
            boja(i,j,2) = 0;
            boja(i,j,3) = 0;
        end
    end
end

if RGB == 'G'
    for i = 1:1:sirina
        for j = 1:1:visina
            boja(i,j,1) = 0;
            boja(i,j,3) = 0;
        end
    end
end

if RGB == 'B'
    for i = 1:1:sirina
        for j = 1:1:visina
            boja(i,j,1) = 0;
            boja(i,j,2) = 0;
        end
    end
end


%% komponenta funkcija je uvijek ista

clc
close all
clear all

slika = imread('krava.jpg'); 

% predstavimo sve RGB komponente zasebno 

crvena = komponenta(slika,'R'); 
zelena = komponenta(slika,'G');
plava = komponenta(slika,'B');

% prikazujemo sve slike 
figure(1); 
imshow(crvena);
title('Crvena komponenta'); 

figure(2); 
imshow(zelena); 
title('Zelena komponenta'); 

figure(3); 
imshow(plava); 
title('Plava komponenta');


% spremamo ih u foldere

mkdir('Original_i_Crvena'); 
mkdir('Original_i_Zelena'); 
mkdir('Original_i_Plava'); 

imwrite(slika, 'Original_i_Crvena/original.jpg'); 
imwrite(crvena, 'Original_i_Crvena/crvena.jpg');

imwrite(slika, 'Original_i_Zelena/original.jpg'); 
imwrite(zelena, 'Original_i_Zelena/zelena.jpg');

imwrite(slika, 'Original_i_Plava/original.jpg'); 
imwrite(plava, 'Original_i_Plava/plava.jpg');




GUI : OVO JE ZA TROSTRANU PIRAMIDU

% Button pushed function: PrikazipiramiduButton
        function PrikazipiramiduButtonPushed(app, event)
         height = app.VisinaPiramideEditField.Value;
        baseLength = app.DuzinaOsnoviceEditField.Value;

        % Calculate the vertices of the tetrahedron
        A = [0, 0, 0];
        B = [baseLength, 0, 0];
        C = [baseLength/2, baseLength*sqrt(3)/2, 0];
        D = [baseLength/2, baseLength*sqrt(3)/6, height];

        % Define the faces of the tetrahedron
        faces = [
            1, 2, 3;
            1, 3, 4;
            1, 4, 2;
            2, 3, 4
        ];

        % Plot the tetrahedron
        cla(app.UIAxes); % Clear previous plot
        hold(app.UIAxes, 'on');
        patch(app.UIAxes, 'Vertices', [A; B; C; D], 'Faces', faces, 'FaceColor', 'magenta', 'EdgeColor', 'k');
        view(app.UIAxes, 3); % Set 3D view
        axis(app.UIAxes, 'equal'); % Set equal axis scales
        xlabel(app.UIAxes, 'X');
        ylabel(app.UIAxes, 'Y');
        zlabel(app.UIAxes, 'Z');
        title(app.UIAxes, 'Tetrahedron');
        hold(app.UIAxes, 'off');
        end
    end
 

CISTI TON GENERISATI
% Step 1: Generate a clean tone of 100 Hz for 1 second at 3000 Hz sampling rate
fs1 = 3000; % Sampling frequency for the tone
t1 = 0:1/fs1:1-1/fs1; % Time vector for 1 second
tone = sin(2*pi*100*t1); % Generate the 100 Hz tone

% Step 2: Generate white noise for 2 seconds at 1000 Hz sampling rate
fs2 = 1000; % Sampling frequency for the noise
t2 = 0:1/fs2:2-1/fs2; % Time vector for 2 seconds
noise = randn(size(t2)); % Generate white noise

% Step 3: Combine the clean tone and the white noise
% Ensure both signals are of the same length by padding the shorter one with zeros
if length(tone) < length(noise)
    tone = [tone zeros(1, length(noise) - length(tone))];
elseif length(noise) < length(tone)
    noise = [noise zeros(1, length(tone) - length(noise))];
end

combined_signal = tone + noise;

% Step 4: Mix the combined signal with a sinusoidal signal
t_combined = 0:1/fs1:(length(combined_signal)-1)/fs1; % Time vector for combined signal
sinusoid = 0.5 * sin(2 * pi * t_combined); % Generate the sinusoidal signal
mixed_signal = combined_signal + sinusoid;

% Step 5: Display all the sound signals
subplot(4, 1, 1);
plot(t1, tone);
title('100 Hz Tone');

subplot(4, 1, 2);
plot(t2, noise);
title('White Noise');

subplot(4, 1, 3);
plot(t_combined, combined_signal);
title('Combined Signal');

subplot(4, 1, 4);
plot(t_combined, mixed_signal);
title('Mixed Signal');

% Play the sounds
sound(tone, fs1);
pause(1);
sound(noise, fs2);
pause(2);
sound(combined_signal, fs1);
pause(length(combined_signal)/fs1);
sound(mixed_signal, fs1);


DODATNI ZADACI


1. SESTOUGAO KOJI SE OKRECE
 
t=(1/12:1/6:1)'*2*pi;
x=sin(t)+1;
y=cos(t)+2;
h=fill(x,y,'k');
axis([0 10 -10 10])


xp=x
yp=y
xc=1
yc=1
for i=1:70
    xp=xp+0.1;
    yp=yp+0.01;
    xc=xc+0.1;
    yc=yc+0.01;
    set(h,'x',xp,'y',yp)
    rotate(h,[0 0 1],i*30,[xc,yc,0])
    pause(0.1)
end





2. KOCKA IDE LIEJVO DESNO
 
%% Kretanje tijela 

clc 
close all
clear all 
% prvo definisemo crveni pravouganik
x = [0 1 1 0];
y = [1 1 2 2];
cp = patch(x,y,'r'); 
% nakon toga definisemo i plavi pravougaonik
x = [0 8 8 0]; 
y = [0 0 1 1]; 
pp = patch(x,y,'b'); 
axis([0 8 0 8]);
pause

x1 = [0 1 1 0]; 
y1 = [1 1 2 2]; 




for i = 1:90
    x1 = x1 + 7/90; 
    set(cp,'x',x1,'y',y1); 
    pause(0.5/90)
end 
for i = 1:60
    x1 = x1 - 7/60; 
    set(cp,'x',x1,'y',y1);
    pause(0.5/60)
end


3. Spojiti zvučne signale upotrebom operatora konkatanacije toms.wav i tenor-sax.wav i prikazati ih upotrebom naredbe plot. 

[zvuk 1,fs]=wavread( 'toms.wav' ); 
[zvuk2,fs]=wavread( 'tenorsax.wav');
 spojeni = [zvuk 1; zvuk2];
t=0:1/fs:1/fs* (length(spojeni)-1);
plot(t,spojeni)
xlabel('Vrijeme[s]')
ylabel('Amplituda')

4. % Izvršiti miksanje zvučnog signala toms.wav sa sinusnim signalom.x=0.5sin(2pi t).
Prikazati ulazne i izlazni zvučni signal.

zvuk1= 'toms.way';
[y, FS]= wavread(zvuk1); 
t=0:1/Fs:1/Fs* (length(y)-1); 
sinusnisignal = 0.5*sin(2*pi*t)'; 
novisignal = y + sinusnisignal;
subplot(3,1,1), plot(t,y, 'linewidth',2)
title('Ulazni signal' );
ylabel('Amplituda' )
subplot(3,1,2), plot(t,sinusnisignal, 'r', 'linewidth',2)
title('Sinusni signal' );
ylabel('Amplituda')
subplot(3,1,3), plot(t,novisignal, 'g', 'linewidth',2)
title('Miksani signal' );
xlabel('Vrijeme[s]')
ylabel('Amplituda')



5. jednacine sa uslvima 
syms x y(x)
jed1 = (1 + x^2) * diff(y, x) == x * (2 * y + 1);
jed2 = x* diff(y,x) - (y)/(x+1) == x;
rj_jed1 = dsolve(jed1);
uslov_2=y(0)==-1;
rj_jed2 = dsolve(jed2);
disp(rj_jed1)
disp(rj_jed2)
sound(mixed_signal, fs1);
