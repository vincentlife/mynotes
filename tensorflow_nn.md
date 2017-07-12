# rnn_cell
## BasicLSTMCell
It(BasicLSTMCell) does not allow cell clipping, a projection layer, and does not use peep-hole connections: it is the basic baseline.
## LSTMCell

# dynamic_rnn

# bidirectional_dynamic_rnn

(max_time, batch_size, cell_fw.hidden_size)

# raw_rnn
## 参数
    raw_rnn( cell, loop_fn, parallel_iterations=None, swap_memory=False, scope=None)
## 返回值
 A tuple (emit_ta, final_state, final_loop_state)
* emit_ta: The RNN output TensorArray
* final_state: The final cell state.
* final_loop_state: The final loop state as returned by loop_fn.

## loop_fn
tf.nn.raw_rnn 最重要的就是 loop_fn 函数的编写，loop_fn做了一个映射
> (time, previous_cell_output, previous_cell_state, previous_loop_state) -> (elements_finished, input, cell_state, output, loop_state).

loop_fn调用的时机有2个：
1. Initial call at time=0 to provide initial cell_state and input to RNN.
2. Transition call for all following timesteps where you define transition between two adjacent steps.



# seq2seq
## tf.contrib.sequence_loss
sequence_loss(logits, targets, weights,
                  average_across_timesteps=True, average_across_batch=True,
                  softmax_loss_function=None, name=None)
### logits: 
shape [batch_size, sequence_length, num_decoder_symbols], 
* batch_size 指batch大小
* sequence_length 序列长度，指num_steps
* num_decoder_symbols 指输出词库的大小vocab_size
### targets | weights
shape [batch_size, sequence_length]
### 
sequence_loss_by_example的做法是，针对logits中的每一个num_step,即[batch_size, vocab_size], 对所有vocab_size个预测结果，得出预测值最大的那个类别，与target中的值相比较计算Loss值

# tensor board
## Visualizing Learning

## Embedding Visualizing