function [en_1_2,en_2_1,dist1,dist2]=calculate_mutual_information(X,Y,pis,j)
%% parpare some data that use in reconstruction phase space
d_x=[];    sit=size(X);
disp(sit)
% templ=randperm((sit(1,1)-1));
% select=templ(1:j);
select=1:j;
% disp(select+1)
% disp(select)
d_x(:,1)=X(select+1,1);d_x(:,2)=X(select,1);d_x(:,3)=Y(select+1,1);d_x(:,4)=Y(select,1);
X_max=max(X(:,1));X_min=min(X(:,1));Y_max=max(Y(:,1));Y_min=min(Y(:,1));
delta1=(X_max-X_min)/(2*pis);delta2=(Y_max-Y_min)/(2*pis);
% figure(1)
% plot(d_x(:,2),d_x(:,1),'MarkerSize',10,'Color','r');
% figure(2)
% plot(d_x(:,4),d_x(:,3),'MarkerSize',10,'Color','b');
%% calculate the data disturbution every prameter
L1=linspace(X_min+delta1,X_max-delta1,pis);L2=linspace(Y_min+delta2,Y_max-delta2,pis);
dist1=zeros(pis,2);
for q1=1:pis
    k1=L1(q1);k2=L2(q1);
    count1=0;count2=0;
    for i=1:j
        if d_x(i,1)>=(k1-delta1) && d_x(i,1)<=(k1+delta1)
            count1=count1+1;
        end
        if d_x(i,3)>=(k2-delta2) && d_x(i,3)<=(k2+delta2)
            count2=count2+1;
        end
    end
    dist1(q1,1)=count1;dist1(q1,2)=count2;
end

dist1(:,1)=dist1(:,1)/sum(dist1(:,1));dist1(:,2)=dist1(:,2)/sum(dist1(:,2)); 

dist2=zeros(pis,pis,1);
for q1=1:pis
    for q2=1:pis
        k1=L1(q1);k2=L1(q2);
        k3=L2(q1);k4=L2(q2);
        count1=0;count2=0;
        for i1=1:j
                if d_x(i1,1)>=(k1-delta1) && d_x(i1,1)<=(k1+delta1) && d_x(i1,3)>=(k4-delta2) && d_x(i1,3)<=(k4+delta2)
                    count1=count1+1;
                end
        end        
        dist2(q1,q2,1)=count1;        
    end
end
dist2(:,:,1)=dist2(:,:,1)/sum(sum(dist2(:,:,1)));
%% use the dosturbution calculate thansfer entropy
sum_f_1=0;sum_f_2=0;
for k1=1:pis
    if dist(k1,1)~=0
        sum_f_1=sum_f_1-dist1(k1,1)*log2(dist1(k1,1));
        sum_f_2=sum_f_2-dist1(k1,2)*log2(dist1(k1,2));
    end
end
disp(sum_f_1);
disp(sum_f_1);
sum_s_1=0;sum_s_2=0;
for k1=1:pis
    for k2=1:pis
        if dist2(k1,k2,1)~=0 && dist1(k2,2)~=0  
           sum_s_1=sum_s_1-dist2(k1,k2,1)*log2(dist2(k1,k2,1)/dist1(k2,2));
           sum_s_2=sum_s_2-dist2(k1,k2,1)*log2(dist2(k1,k2,1)/dist1(k1,1));
        end
        
    end
end
disp(sum_s_1);
disp(sum_s_2);

en_1_2=sum_f_1-sum_s_1;
en_2_1=sum_f_2-sum_s_2;
end
