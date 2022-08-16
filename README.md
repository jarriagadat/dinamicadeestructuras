# Edificio Tipo Corte  
Jorge Arriagada, Universidad de Valparaíso
v2022.06


![image](https://user-images.githubusercontent.com/5865486/177553091-db3d8668-2853-4172-81b5-9a573c50390a.png)

Ref: Paz, M. (1991). Structural Dynamics. Springer, Boston, MA. https://doi.org/10.1007/978-1-4684-9907-0_9.


Estructura
```
N = 5     % N pisos
m = 100
Kc = 1000
```

MATRIZ DE MASA [M]
```
M=zeros(N,N);
for i=1:N %piso
    for j=1:N %columna
        if i==j
            M(i,j)=m;  
        end
    end  
end  
M
```

MATRIZ DE RIGIDEZ
```
% Rigidez columna tipo
% Kpiso=12*E*I/L^3 

% MATRIZ DE RIGIDEZ
K=zeros(N,N);
for i=1:N %piso
    for j=1:N %columna
        if i==N & j==N
            K(i,j)=2*Kc;
        elseif i==j
            K(i,j)=4*Kc;  
        elseif abs(i-j)==1
            K(i,j)=-2*Kc;
        else
            K(i,j)=0;
        end
    end  
end  
K
```

FRECUENCIAS DEL SISTEMA

```
% Matriz del sistema
A = inv(M)*K
% phi y w2 son matrices
% la matriz phi son los eigenvectors (modos) y
% la diagonal de la matriz w2 son los eigenvalues (frecuencias)
[phi,w2] = eig(A)

% Ordenar los eigen-values y eigen-vectors
[w2_ord, ind] = sort(diag(w2),'ascend')
phi_ord = phi(:,ind)

pisonorm = 1
% normaliza al modo phi(i,i)
% for i=1:N
%     phi(:,i)=phi(:,i)/phi(i,i);
% end

% normaliza al modo phi(N,i)
for i=1:N
    phi(:,i)=phi_ord(:,i)/phi_ord(pisonorm,i);
end
w=sqrt(w2_ord)
phi
```
