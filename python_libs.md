# pickle
import pickle
**output = open('data.pkl', 'wb')**
pickle.dump(object, output)

pkl_file = open('data.pkl', 'rb')
object = pickle.load(pkl_file)

# feather
用于数据框的快速读写
