原式為$\text{softmax}(z_i) = \frac{e^{z_i}}{\sum_{k=1}^{K} e^{z_k}}$，
$\text{log\_softmax}(z_i) = \log\left(\frac{e^{z_i}}{\sum_{k=1}^{K} e^{z_k}}\right)$，即`log(softmax(z))`經過化簡，
$\text{log\_softmax}(z_i) = z_i - \log\left(\sum_{k=1}^{K} e^{z_k}\right)$。
從而提高計算上的穩定性以及效率。


