```rust
fn bytes_to_giga_bytes(data: u64, decimal: &usize) -> String {
    format!("{:.*}GB", decimal, data as f64 / 1073741824.0)
}

fn bytes_to_mega_bytes(data: u64, decimal: &usize) -> String {
    format!("{:.*}MB", decimal, data as f64 / 1048576.0)
}

fn bytes_to_kilo_bytes(data: u64, decimal: &usize) -> String {
    format!("{:.*}KB", decimal, data as f64 / 1024.0)
}

#[test]
fn test_byte_conversions() {
    let data: u64 = 6846158942;
    let decimal: &usize = &2;

    let gigabytes: String = bytes_to_giga_bytes(data, decimal);
    let kilobytes: String = bytes_to_mega_bytes(data, decimal);
    let megabytes: String = bytes_to_kilo_bytes(data, decimal);

    assert_eq!(gigabytes, "6.38GB");
    assert_eq!(kilobytes, "6529.01MB");
    assert_eq!(megabytes, "6685702.09KB");
}
```