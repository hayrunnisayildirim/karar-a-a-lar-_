# karar-a-a-lar-_

data("HairEyeColor")
str(HairEyeColor)
summary(HairEyeColor)
View(HairEyeColor)


HairEyeColor <- as.data.frame(HairEyeColor)
attach(HairEyeColor)
str(HairEyeColor)
agac<- J48(Sex ~ ., data = HairEyeColor)
print(agac)
summary(agac)
plot(agac)

agac2<- J48(Hair ~ ., data = HairEyeColor) 
print(agac2)
summary(agac2)
plot(agac2)

agac3<- J48(Eye ~ ., data = HairEyeColor)
print(agac3)
summary(agac3)
plot(agac3)

View(HairEyeColor)
HairEyeColor$Freq <- NULL

attach(HairEyeColor)
str(HairEyeColor)
agac<- J48(Sex ~ ., data = HairEyeColor)
print(agac)
summary(agac)
plot(agac)

agac2<- J48(Hair ~ ., data = HairEyeColor) 
print(agac2)
summary(agac2)
plot(agac2)

agac3<- J48(Eye ~ ., data = HairEyeColor)
print(agac3)
summary(agac3)
plot(agac3)




#C4.5 karar agaclari uygulamasi
#RWeka Kullanilacak
#Bu paketi kurabilmek icin java yazilimi ve rJava isimli paketi kuralim
## ONdan once ekstra
# bir veri setinde NA degerlerini silmek icin
# veriler <- na.omit(veriler)
na.omit()

# veri setinde kayip deger var mi?
#anyNA()

## ayrica verileri hizlica normalize etmek icin scale
# veriler<- scale(veriler)


install.packages("rJava")
install.packages("RWeka")
library(RWeka)

#iris veri setini kullanacagiz
#ilk alti gozlem degerine bakalim
#bunun icin head fonksiyonunu kullanabiliriz
head(iris)
data(iris)
View(iris)

anyNA(iris)

#veri kumesinin herbir degiskeni veri madenciliginde oznitelik "atribute" olarak isimlendirilir.
str(iris)
summary(iris)
attributes(iris)

#Rweka paketi icinde C4.5  algoritmasinin J48() 
#isimli bir uyarlamasi yer almaktadir. 
kararagacimodeli <- J48(Species ~ ., data = iris)

#kurallari gorelim
print(kararagacimodeli)

summary(kararagacimodeli)

#grafigini cizelim eger grafik cikmaz ize partykit yukleyin
plot(kararagacimodeli)

#ongoru icin predict fonksiyonundan yararlanacagiz

ongoru <- predict(kararagacimodeli)

ongoru [1:150]

#eger gercek veriler ile ongoru sonuclari birlikte gorulmek istenirse

data.frame(Species=iris$Species, ongoru=ongoru)[1:150,]

#yeni bir iris cicegi verisi geldiginde hangi sinifa gidecek tahmin edelim

yeni <- data.frame( Sepal.Length=4.1, Sepal.Width =3.2, Petal.Length=1.5, Petal.Width=1.2 )

#bu yeni gozlem degerinin hangi tur oldugunu bulalim
predict(kararagacimodeli,yeni)

