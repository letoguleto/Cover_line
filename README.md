<p><b>Task:</p></b>
По данным n отрезкам необходимо найти множество точек минимального размера, для которого каждый из отрезков содержит хотя бы одну из точек.

В первой строке дано число 1 ≤ n ≤ 100 отрезков. Каждая из последующих n строк содержит по два числа 0 ≤ l ≤ r ≤109, задающих начало и конец отрезка. Выведите оптимальное число m точек и сами m точек. Если таких множеств точек несколько, выведите любое из них.
<pre>
  <code>
<b>simple input:</b>
3
1 3
2 5
3 6
</pre>
  </code>
<pre>
  <code>
<b>simple output:</b>
2
3 6
</div>
</pre>
  </code>

<p><b>Решение(Solution)<p><b>
<pre>
  <code>
#include <stdio.h>
#include <stdlib.h>  
#include <vector>

void sort(std::vector<int*>*);
std::vector<int>* pointSearch(std::vector<int*>);

void sort(std::vector<int*>* vec) {
    int* temp = nullptr;
    for(int i = 0;i < vec->size();i++){
        for(int j = i;j < vec->size();j++){
            if (vec->at(i)[1] > vec->at(j)[1]){
                temp = vec->at(j);
                vec->at(j) = vec->at(i);
                vec->at(i) = temp;
                //printf("its f %d its sc %d\n",temp[0],temp[1]);
            }
        }
    }
}

std::vector<int>* pointSearch(std::vector<int*> vec){//возвращение указателя на верктор точек
    std::vector<int>* pointVec = new std::vector<int>;

    while(vec.size() != 0){
        int* currentPoint = vec[0];
        pointVec->push_back(currentPoint[1]);
        while(true){
            if(!vec.empty() && (*vec.begin()[0] <= currentPoint[1]))
                vec.erase(vec.begin());
            else break;
        }
    }
    //printf("currentPoint[0] %d currentPoint[1] %d\n",currentPoint[0],currentPoint[1]);
    return pointVec;
}
int main()
{
    int countLines;
    std::vector<int*>storage = {};
    scanf("%d", &countLines);

    for (int i = 0; i < countLines; i++) {
        int* p = new int;
        scanf("%d %d",&p[0],&p[1]);
        storage.push_back(p);
        //printf("%d\n",*(storage[i]));
    }
    sort(&storage);

    std::vector<int>* pointStorage = pointSearch(storage);
    ///////////////////////////////
    printf("%d\n",pointStorage->size());
    for(auto & i : *pointStorage){
        printf("%d ",i);
    }


    for(int i =0;i < storage.size();i++){
        delete(storage.at(i));
    }
    delete pointStorage;


    return 0;
}
</code>
</pre>
