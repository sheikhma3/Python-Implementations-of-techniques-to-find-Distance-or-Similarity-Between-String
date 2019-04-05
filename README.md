# Python-Implementations-of-techniques-to-find-Distance-or-Similarity-Between-String
In this Implementation we have code many techniques to find the distance or similarity between strings. Techniques that we explore and Implemented in Python are (word-level &amp; character-level) Minimum Edit Distance, Euclidean Distance, Manhattan Distance, Chebychev Distance, Cosine Similairty, bigram-level Jaccard Similarity Hamming Distance and Longest Common Subsequence Algorithms.
Implementaion includes the code with comments in simple understanding where you can run any of them to find the Similarity or disimilarity between two strings/words. 
Techniques which we have explored are the following:

<h3>Euclidean Distance</h3>

Good choice for numeric attributes When data is dense or continuous, this is a good proximity
measure
 
 The Pythagorean theorem gives this distance between two
points, p and q, each with a n-dimensional feature vector:
   
   
       def eclidian(vec1,vec2):
            #print(vec1)
            #print(vec2)
            dist=math.sqrt(sum([(a - b) ** 2 for a, b in zip(vec1, vec2)]))
            return dist
            
<h3>Manhatten Distance</h3>

The distance between two points is the sum of the absolute
differences of their Cartesian coordinates.
– It is the total sum of the difference between the x-coordinates
and y-coordinates.
Also known as Manhattan length, rectilinear distance, L1
distance or L1 norm, city block distance, snake distance,
taxi-cab metric, or city block distance

      𝑑 (𝑝, 𝑞) = 𝑑( 𝑞, 𝑝) = |𝑝1 − 𝑞1| + |𝑝2 − 𝑞2| ,....... , |𝑝𝑛 − 𝑞𝑛|


      def manhattan(vec1,vec2):
          dist=sum([np.abs(a - b) for a, b in zip(vec1, vec2)])
          return dist
          
<h3> Chebyshev Distance </h3>
For Chebyshev distance, the distance between two vectors is the greatest of their differences along any coordinate dimension.

      def Chebychef(vec1,vec2):
          dist= np.max(np.absolute(np.array(vec1) - np.array(vec2)))
          return dist
          
<h3> Cosine Similarity </h3>
Cosine Similarity of two strings can be caluculated by thaking dot product of their vectors..


        def cosine_similarity(v1,v2):
            sumxx, sumxy, sumyy = 0, 0, 0
            for i in range(len(v1)):
                x = v1[i]; y = v2[i]
                sumxx += x*x
                sumyy += y*y
                sumxy += x*y
            return sumxy/math.sqrt(sumxx*sumyy)

<h3> Jaccard Similarity </h3>

        def Jaccard_similarity(v1,v2):
            v1_bigram=make_bigram(v1)
            v2_bigram=make_bigram(v2)
            dist=len(set(v1_bigram).intersection(set(v2_bigram)))/len(set(v1_bigram).union(set(v2_bigram)))
            return dist


<h3>  Hamming Distance </h3>

        def Hamming_Dist(str1,str2):
            dist=0.0
            str1_set=set()
            str2_set=set()
            for i in range(0,len(str1)):
                str1_set.add(str1[i])
            #print(str1_set)
            for i in range(0,len(str2)):
                str2_set.add(str2[i])
            #print(str2_set)
            Num_of_same_char=len(str1_set.intersection(str2_set))
            #print(Num_of_same_char)
            if len(str1_set)>=len(str2_set):
                dist=len(str1_set)-Num_of_same_char
                #print(len(str1_set))
            if len(str2_set)>len(str1_set):
                dist=len(str2_set)-Num_of_same_char

            return dist

<h3> Minimum Edit Distance </h3>

Levenshtein Distance
– No. of edits between two words/strings – Costs • Insertion = Deletion = 1 • Substitution = insertion + deletion = 2 (except substitution of identical characters, which costs 0) – E.g. from
    I N T E N * T I O N
    * E X E C U T I O N
    D S S S I = 8
Set the cost in .ipynb file in following cell: del_cost=1 ins_cost=1 sub_cost=2

Then pass the strings in Function Parameter. It will output the minimun edit distance between the strings. There are two params in function source string and destination string

          #Character Based Distance
          def Calculate_Minimum_edit_distance(source,target):    
              n= len(source)
              m= len(target)
              MED_Matrix= np.zeros((n+1,m+1), dtype='int32')
              for i in range(1,n+1):
                  MED_Matrix[i][0]=MED_Matrix[i-1][0]+del_cost
              for i in range(1,m+1):
                  MED_Matrix[0][i]=MED_Matrix[0][i-1]+del_cost   
              for i in range(1,n+1):
                  for j in range(1,m+1):
                      if(source[i-1]==target[j-1]):
                          MED_Matrix[i][j]=min([MED_Matrix[i-1][j]+del_cost,MED_Matrix[i-1][j-1]+0,MED_Matrix[i][j-1]+ins_cost])
                      else:
                          MED_Matrix[i][j]=min([MED_Matrix[i-1][j]+del_cost,MED_Matrix[i-1][j-1]+sub_cost,MED_Matrix[i][j-1]+ins_cost])
              #print(np.matrix(MED_Matrix))
              #print(MED_Matrix[n][m])
              return MED_Matrix[n][m]
              
              
<h3> Longest Subsequence </h3>


        def longestsubseq(str1 , str2): 

            m = len(str1) 
            n = len(str2) 
            L = [[None]*(n+1) for i in range(m+1)] 
            for i in range(m+1): 
                for j in range(n+1): 
                    if i == 0 or j == 0 : 
                        L[i][j] = 0
                    elif str1[i-1] == str2[j-1]: 
                        L[i][j] = L[i-1][j-1]+1
                    else: 
                        L[i][j] = max(L[i-1][j] , L[i][j-1]) 


            return L[m][n] 
