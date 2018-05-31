# coolstuff


## Task 3 vienas iš testų

```c++
TEST(rusiavimas, rs){
    vector<Studentas> studentai, geek;
    Nuskaitymas(studentai, "test.txt");
    EXPECT_EQ(studentai.size(), 10);
    ArKietas(studentai,geek,true);
    EXPECT_EQ(studentai.size(), 1);
    EXPECT_EQ(geek.size(), 9);
    EXPECT_EQ(studentai[0].vardas(), "Pavarde1");
}
```


## Vector Emplace

```c++


    template< class... Args >
    iterator emplace( const_iterator pos, Args&&... args ){

        auto position = std::distance(cbegin(),pos);
        if (sz == cap){
            if (cap == 0) cap = 1;
            else cap *= 2;
            value_type* n_elem = allocatorius.allocate(cap);
            std::move(elem,elem+position,n_elem);
            allocatorius.construct(n_elem + position, std::forward<Args>(args)...);
            std::move(elem + position, elem + sz, n_elem + position + 1);
            allocatorius.deallocate(elem, sz);
            elem = n_elem;
        } else{
            std::move(elem + position, elem + sz, elem + position + 1);
            allocatorius.construct(elem + position, std::forward<Args>(args)...);
        }
        sz++;
        return &elem[position];
    }
```

### Release -o3

|Duomenu kiekis                    |PVector     |std::vector     |
|----------------------------------|-----------------|----------------|
| n = 10000 | 0.00548556 s. | 0.00039869 s. |
| n = 100000 | 0.00189481 s. | 0.00249188 s. |
| n = 1000000 | 0.00718079 s. | 0.0206307 s. |
| n = 10000000 | 0.0839762 s. | 0.195894 s. |
| n = 100000000 | 0.867825 s. | 2.07747 s. |
