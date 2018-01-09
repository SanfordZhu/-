# MP_algorithm
dictionary = [-0.707 0.707;0.8 0.6;0 -1]';  
x = [1.65 -0.25]';  
[M,N] = size(dictionary);  
residual = zeros(M);%残差矩阵，保存每次迭代后的残差  
residual(:,1) = x;%初始化残差为x  
L = size(residual,2);%得到残差矩阵的列  
pos_mm = zeros(1,L);%用来保存每次选择的列序号  
resi_norm = zeros(1,L);%用来保存每次迭代后的残差的2范数  
resi_norm(1) = norm(x);%因为前面已初始化残差为x  
reconstuction=zeros();
reconstuction1=zeros();
for mm = 1:7
    %求出dictionary每列与上次残差的内积  
    scalarproducts = dictionary'*residual(:,mm);  
    %找到内积中最大的列及其内积值  
    [val,pos] = max(abs(scalarproducts));  
    %赋值给重构的系数
    reconstuction(:,mm)=val;
    %每个系数对应选择的原子
    reconstuction1(:,mm)=pos;
    %更新残差  
    residual(:,mm+1) = residual(:,mm) - ... 
        scalarproducts(pos)*dictionary(:,pos);  
    %计算残差的2范数（平方和再开根号）  
    resi_norm(mm+1) = norm(residual(:,mm+1));  
    %保存选择号  
    pos_mm(mm+1) = pos;  
end  
%绘出残差的2范数曲线  
plot(resi_norm);grid;  
%生成重构后每一次选择对应的原子
reconstuction1
%生成重构后的原子系数
reconstuction
