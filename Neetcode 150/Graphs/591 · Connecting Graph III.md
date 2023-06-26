#### Lintcode: 591 · Connecting Graph III
class ConnectingGraph3:
    """
    @param a: An integer
    @param b: An integer
    @return: nothing
    """
    def __init__(self, n):
        self.size = n
        self.father = {}
        for i in range(1, n + 1):
            self.father[i] = i
    
    def connect(self, a, b):
        root_a = self.find(a)
        root_b = self.find(b)
        if root_a != root_b:
            self.father[root_a] = root_b
            self.size -= 1

    def query(self):
        return self.size
    
    def find(self, node):
        path = []
        while node != self.father[node]:
            path.append(node)
            node = self.father[node]
        
        for n in path:
            self.father[n] = node
        return node