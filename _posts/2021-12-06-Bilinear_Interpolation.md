### Producing exact result like a Bilinear Interpolation Method

num_rows = img_gray.shape[0]
num_cols = img_gray.shape[1]

*setting the scaling matrix*

S = np.array([[2,0],[0,2]])

*making the size of the destination image double than the source image*

img_doubled = np.zeros((2*num_rows,2*num_cols),dtype='uint8')

*computing the inverse matrix*

S_inv = np.linalg.inv(S)

*we shall be looping over the destination image*

for new_row in range(img_doubled.shape[0]):
    for new_col in range(img_doubled.shape[1]):
        p_dash = np.array([new_row,new_col])
        p = S_inv.dot(p_dash)
        
        
       
   *applying the floor and ceil method to get the 4 corners of the discrete pixels surrounding pixel p*
       
        p_floor = np.int16(np.floor(p))
        p_ceil = np.int16(np.ceil(p))
   
   *get the actual position of the pixels in the source image*
   
        row = p[0]
        col = p[1]   
   *get the 4 bounding corners*
        
        row_min,col_min = p_floor[0],p_floor[1]
        row_max,col_max = p_ceil[0],p_ceil[1]            
   *actual position of the pixel in the source image*
   
        point = (row,col)
   *storing the values of 4 bounding corners as the variables in the form of coordinates for distance computation*
       
        cor00 = (row_min,col_min)
        cor01 = (row_max,col_min)
        cor10 = (row_min,col_max)
        cor11 = (row_max,col_max   
   *compute the distince of pixel p with each of the 4 bounding corners*
        
        w00 = distance.euclidean(point, cor00)
        w01 = distance.euclidean(point, cor01)
        w10 = distance.euclidean(point, cor10)
        w11 = distance.euclidean(point, cor11)
   *since weight could be zero, to handle divide by zero casse, we replace 0 with 1 if any*   
        
        if w00==0:
            w00=1
        if w01==0:
            w01=1
        if w10==0:
            w10=1
        if w11==0:
            w11=1
   *compute the sum of weight, where weight is just the inverse of the distance i.e greater the distance smaller the weight and vice versa*
            
        sum_weight = (1/w00)+(1/w01)+(1/w10)+(1/w11)
        
   *performing a boundary check*
   
        if row_min<0 or row_max>=num_rows or col_min<0 or col_max>=num_cols:
            pass
        else:
   *display the image*
         
            img_doubled[new_row,new_col] = np.round((img_gray[row_min,col_min]*(1/w00)+img_gray[row_max,col_min]*(1/w01)+img_gray[row_min,col_max]*(1/w10)+img_gray[row_max,col_max]*(1/w11))/(sum_weight))

