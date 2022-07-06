# Edificio Tipo Corte  
Jorge Arriagada, Universida de Valparaíso
v2022.06


![image](https://user-images.githubusercontent.com/5865486/177553091-db3d8668-2853-4172-81b5-9a573c50390a.png)

Ref: Paz, M. (1991). Structural Dynamics. Springer, Boston, MA. https://doi.org/10.1007/978-1-4684-9907-0_9.


### MATRIZ DE MASA [M]
M=zeros(N,N);
for i=1:N %piso
    for j=1:N %columna
        if i==j
            M(i,j)=m;  
        end
    end  
end  
M
